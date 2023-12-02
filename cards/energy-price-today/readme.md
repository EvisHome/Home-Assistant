# Energy Spot Price for Today and Energy Usage

![image](https://github.com/EvisHome/Home-Assistant/assets/98347572/df2e72f6-9481-40de-bfad-c7e8a3ed308c)

* Nordpool integration
* Shelly 3EM for home total power measurement
* custom:config-template-card
* custom:apexcharts-card


### Template Sensors

```YAML
  ## HOME TOTAL POWER
- platform: template
  sensors:
    home_total_power:
      friendly_name: "Home Total Power"
      unit_of_measurement: "W"
      value_template: >-
        {{ states('sensor.home_energy_shelly_3em_channel_a_power')|float + states('sensor.home_energy_shelly_3em_channel_b_power')|float + states('sensor.home_energy_shelly_3em_channel_c_power')|float }}
```



### Calculating the High and Low price values for graph colors

```YAML
    nordpool_today_mean_hi_limit:
      unit_of_measurement: "c"
      friendly_name_template: "Nordpool Today Average High Limit"
      value_template: >
        {{ state_attr('sensor.nordpool_kwh_fi_eur_3_10_024', 'mean')|float * 0.15 + state_attr('sensor.nordpool_kwh_fi_eur_3_10_024', 'mean')|float }}

    nordpool_today_mean_lo_limit:
      unit_of_measurement: "c"
      friendly_name_template: "Nordpool Today Average Low Limit"
      value_template: >
        {{ state_attr('sensor.nordpool_kwh_fi_eur_3_10_024', 'mean')|float - (0.15 * state_attr('sensor.nordpool_kwh_fi_eur_3_10_024', 'mean')|float) }}

```



### The Card

```YAML
type: custom:config-template-card
variables:
  PRICEHIGH: states['sensor.nordpool_today_mean_hi_limit'].state
  PRICELOW: states['sensor.nordpool_today_mean_lo_limit'].state
entities:
  - sensor.nordpool_kwh_eur_without_tax
card:
  type: custom:apexcharts-card
  graph_span: 1d
  span:
    start: day
  apex_config:
    stroke:
      dashArray: 4
    chart:
      height: 180px
      width: 115%
      offsetX: -30
    title:
      text: Energy Price Today
      align: center
      offsetY: 10
      style:
        fontSize: 13px
        fontFamily: Verdana
        fontWeight: normal
    grid:
      show: true
      borderColor: rgba(255,255,255,0.2)
    xaxis:
      position: bottom
      labels:
        format: H
        hideOverlappingLabels: true
        offsetX: 0
      axisTicks:
        offsetX: 0
    legend:
      show: false
      itemMargin:
        vertical: 10
        horizontal: 10
    tooltip:
      enabled: false
      style:
        fontSize: 14px
  show:
    last_updated: true
  experimental:
    color_threshold: true
  header:
    show_states: true
    colorize_states: true
  now:
    show: true
  yaxis:
    - id: cost
      #min: 0 # Uncomment this for have cost Y-axis to start from 0
      opposite: true
      decimals: 1
      apex_config:
        tickAmount: 4
        labels:
          show: true
        title:
          text: c/kWh
          rotate: 0
          offsetX: -25
          offsetY: -70
          style:
            fontSize: 10px
            fontFamily: verdana
            color: orange
    - id: energy
      max: ~2
      min: 0
      decimals: 1
      apex_config:
        tickAmount: 4
        labels:
          show: true
        title:
          text: kWh
          rotate: 0
          offsetX: 25
          offsetY: -70
          style:
            color: skyblue
            fontSize: 10px
            fontFamily: verdana
  series:
    - entity: sensor.nordpool_kwh_fi_eur_3_10_024
      name: Price
      yaxis_id: cost
      type: column
      opacity: 0.8
      stroke_width: 0
      show:
        extremas: true
        in_header: raw
        header_color_threshold: true
      data_generator: |
        return entity.attributes.raw_today.map((start, index) => {
          return [new Date(start["start"]).getTime(), entity.attributes.raw_today[index]["value"]];
        });
      color_threshold:
        - value: 1
          color: lightgreen
        - value: ${PRICELOW * 1}
          color: orange
        - value: ${PRICEHIGH * 1}
          color: darkred
    - entity: sensor.home_total_energy_hourly
      name: Energy (kWh)
      color: skyblue
      type: line
      opacity: 1
      yaxis_id: energy
      stroke_width: 2
      float_precision: 1
      extend_to: false
      unit: kWh
      group_by:
        duration: 1hour
        func: max
      show:
        legend_value: false
        datalabels: false
```

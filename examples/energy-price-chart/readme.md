type: custom:config-template-card
variables:
  PRICEAVERAGE: states['sensor.nordpool_kwh_fi_eur_3_10_024'].attributes['average']
  PRICEMEAN: states['sensor.nordpool_kwh_fi_eur_3_10_024'].attributes['mean']
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
      width: 120%
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


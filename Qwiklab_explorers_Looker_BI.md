# Analyze Customer Reviews with Gemini Using Python Notebooks || [GSP1249](https://www.cloudskillsboost.google/focuses/98857?parent=catalog) || 

## # Like, comment, share & Don't forget to subscribe [QwikLab Explorers](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

---
## ⚠️ **Disclaimer:**
#### This script and guide are provided for educational purposes to help you understand the lab process. Please ensure you understand the steps before using any scripts. Before using the script, I encourage you to open and review it to understand each step.The goal is to help you learn how to complete the labs effectively while following Qwiklabs' terms of service and YouTube's community guidelines.

---
### 🚨 First, click the toggle button to turn on the Development mode.
---

- Go to Develop > qwiklabs-flights-maps > general > flights
- Open qwiklabs-flights-maps.model file
> Replace the below commands on here!!
```
connection: "bigquery_public_data_looker"
# include all views in this project
include: "*.view"
include: "/z_tests/*.lkml"

map_layer: data_area {
  file: "maps/US_West_Midwest.topojson"
}

explore: airports {
  group_label: "FAA"
}

explore: flights {
  group_label: "FAA"
  description: "Start here for information about flights!"
  join: carriers {
    type: left_outer
    sql_on: ${flights.carrier} = ${carriers.code} ;;
    relationship: many_to_one
  }

  join: aircraft {
    type: left_outer
    sql_on: ${flights.tail_num} = ${aircraft.tail_num} ;;
    relationship: many_to_one
  }

  join: aircraft_origin {
    from: airports
    type: left_outer
    sql_on: ${flights.origin} = ${aircraft_origin.code} ;;
    relationship: many_to_one
    fields: [full_name, city, state, code, map_location]
  }

  join: aircraft_destination {
    from: airports
    type: left_outer
    sql_on: ${flights.destination} = ${aircraft_destination.code} ;;
    relationship: many_to_one
    fields: [full_name, city, state, code, map_location]
  }

  join: aircraft_models {
    sql_on: ${aircraft.aircraft_model_code} = ${aircraft_models.aircraft_model_code} ;;
    relationship: many_to_one
  }
}


# Place in `qwiklabs-flights-maps` model
explore: +flights {
    query: QwikLab_Explorers_1 {
      dimensions: [aircraft_destination.map_location, aircraft_origin.map_location]
      measures: [count]
      filters: [
        aircraft_destination.state: "CA,WA,CO,NV,UT,AK,HI,OR,LA,ID,WY",
        aircraft_origin.city: "ATLANTA^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ",
        flights.arrival_year: "2004"
      ]
  }
}

# Place in `qwiklabs-flights-maps` model

explore: +flights {
    query: QwikLab_Explorers_2 {
      dimensions: [aircraft.region]
      measures: [aircraft.count]
    }
  }


```

- Open the aircraft.view file
> Replace the below commands on here!!

```
    sql: ${TABLE}.cert_issue_date ;;
  }

  dimension: certification {
    type: string
    sql: ${TABLE}.certification ;;
  }

  dimension: city {
    type: string
    sql: ${TABLE}.city ;;
  }

  dimension: country {
    type: string
    map_layer_name: countries
    sql: ${TABLE}.country ;;
  }

  dimension: county {
    type: string
    sql: ${TABLE}.county ;;
  }

  dimension: fract_owner {
    type: string
    sql: ${TABLE}.fract_owner ;;
  }

  # Don't use this one. It complicates the custom measure exercise.
  # Can't just hide it because hidden fields still show up as suggestions in custom fields.
  # dimension_group: last_action {
  #   hidden: yes
  #   type: time
  #   timeframes: [time, date, week, month, raw]
  #   convert_tz: no
  #   datatype: date
  #   sql: ${TABLE}.last_action_date ;;
  # }

  dimension: last_action_year {
    type: number
    sql: EXTRACT(YEAR FROM ${TABLE}.last_action_date) ;;
  }

  dimension: mode_s_code {
    type: string
    sql: ${TABLE}.mode_s_code ;;
  }

  dimension: name {
    type: string
    sql: ${TABLE}.name ;;
  }

  dimension: region {
    type: string
    case: {
      when: {
        sql: ${state} in ('WA','OR','CA','NV','UT','WY','ID','MT','CO','AK','HI') ;;
        label: "West"
      }
      when: {
        sql: ${state} in ('AZ','NM','TX','OK') ;;
        label: "Southwest"
      }
      when: {
        sql: ${state} in ('ND','SD','MN','IA','WI','MN','OH','IN','MO','NE','KS','MI','IL') ;;
        label: "Midwest"
      }
      when: {
        sql: ${state} in ('MD','DE','NJ','CT','RI','MA','NH','PA','NY','VT','ME','DC') ;;
        label: "Northeast"
      }
      when: {
        sql: ${state} in ('AR','LA','MS','AL','GA','FL','SC','NC','VA','TN','KY','WV') ;;
        label: "Southeast"
      }
      else: "Unknown"
    }
    map_layer_name: data_area
    drill_fields: [state]
  }


  dimension: registrant_type_id {
    type: number
    sql: ${TABLE}.registrant_type_id ;;
  }

  dimension: state {
    type: string
    sql: ${TABLE}.state ;;
  }

  dimension: status_code {
    type: string
    sql: ${TABLE}.status_code ;;
  }

  dimension: year_built {
    # type: date_year
    # sql: DATE(nullif(${TABLE}.year_built,0), 01, 01) ;;   # makes the SQL too clunky

    type: number
    sql: nullif(${TABLE}.year_built,0) ;;
    value_format_name: id
  }

  dimension: zip {
    type: zipcode
    sql: ${TABLE}.zip ;;
  }

  measure: count {
    type: count
    drill_fields: [name]
  }
}

```

---

## Congratulations ..!!🎉  You completed the lab shortly..😃💯

## *Well done..!* 👏

## Thank you for visiting... :) 🗯️

## [QwikLab Explorers](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)

## Join to our community [Digital Dominators](https://chat.whatsapp.com/J0o1beFGCHfJ8ZHGKjcqkd)

## Stay Connected with Our Community! 💬 

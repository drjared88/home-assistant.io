---
layout: page
title: "Entity Filter Card"
sidebar_label: Entity Filter
description: "This card allows you to define a list of entities that you want to track only when in a certain state. Very useful for showing lights that you forgot to turn off or show a list of people only when they're at home. "
date: 2018-07-01 10:28 +00:00
sidebar: true
comments: false
sharing: true
footer: true
---

This card allows you to define a list of entities that you want to track only when in a certain state. Very useful for showing lights that you forgot to turn off or show a list of people only when they're at home.

This type of card can also be used together with rest of cards that allow multiple entities, allowing you to use [glance](/lovelace/glance/) or [picture-glance](/lovelace/picture-glance/). By default it uses [entities](/lovelace/entities/) card model.

<p class='img'>
<img src='/images/lovelace/lovelace_entity_filter.png' alt='Screenshot of the entity filter card'>
Screenshot of the entity filter card.
</p>

{% configuration %}
type:
  required: true
  description: entity-filter
  type: string
entities:
  required: true
  description: "List of entities to show."
  type: list
  keys:
    name:
      required: false
      description: The name to use in the front for the entity.
      type: string
    entity:
      required: false
      description: "The `entity_id` to show in the frontend."
      type: string
state_filter:
  required: true
  description: Array of strings representing states.
  type: array
card:
  required: false
  description: Extra options to pass down to the card rendering the result.
  type: object
  default: entities type
show_empty:
  required: false
  description: Allows hiding of card when no entities returned by filter.
  type: boolean
  default: true
{% endconfiguration %}

## {% linkable_title Examples %}

Show only active switches or lights in the house
```yaml
- type: entity-filter
  entities:
    - entity: light.bed_light
      name: Bed
    - light.kitchen_lights
    - light.ceiling_lights
  state_filter:
    - 'on'
  card:
    title: Eating power
```

Show only people that are at home using [glance](/lovelace/glance/):

```yaml
- type: entity-filter
  entities:
    - device_tracker.demo_paulus
    - device_tracker.demo_anne_therese
    - device_tracker.demo_home_boy
  state_filter:
    - 'home'
  card: 
    type: glance
    title: People at home
```

<p class='img'>
<img src='/images/lovelace/lovelace_entity_filter_glance.png' alt='Screenshot of the entity filter used on a Glance card'>
Screenshot of the entity filter used on a Glance card.
</p>

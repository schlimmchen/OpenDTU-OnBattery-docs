# MQTT Battery Provider

## Screenshot

![MQTT Battery Settings](../../assets/images/screenshots/battery_settings_mqtt.png)

## Settings / Parameters

### SoC Settings

#### SoC Value Topic :material-form-textbox:{title="Textbox"}

MQTT topic to which the battery SoC value is published on your broker.

#### JSON Path :material-form-textbox:{title="Textbox"}

If the payload of the topic is not a numeric value but a serialized JSON
object, this path expressions tells which value to extract from the JSON
object.

### Voltage Settings

#### Voltage Value Topic :material-form-textbox:{title="Textbox"}

MQTT topic to which the battery voltage value is published on your broker.

#### JSON Path :material-form-textbox:{title="Textbox"}

If the payload of the topic is not a numeric value but a serialized JSON
object, this path expressions tells which value to extract from the JSON
object.

#### Unit :material-form-dropdown:{title="Dropdown"}

Allows to set the actual unit of the numeric voltage payload, often Volt (V)
or Millivolt (mV).

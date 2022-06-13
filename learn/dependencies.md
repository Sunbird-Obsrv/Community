# Dependencies

## Sunbird Telemetry <a href="#sunbird-telemetry" id="sunbird-telemetry"></a>

Sunbird Telemetry is a specification to instrument all the key events. Using this specification reference applications & services will generate telemetry events.

{% hint style="info" %}
Resolution : _Obsrv_ as a building block serves to collect and process telemetry. Just like it works with the Sunbird telemetry spec, it can work seamlessly with any spec that a system may adopt as its choice of reference. The events generated will be in accordance with the spec of choice, and _Obsrv_ can carry out validation and aggregate telemetry accordingly.
{% endhint %}

## Sunbird Lern

The User and Org service of Sunbird Lern is used for obtaining various metadata about the user - including fetching user roles & privileges to authenticate exhaust requests.

{% hint style="info" %}
Resolution: _Obsrv_ uses the meta data provided by the _Lern_ building block in order to gather user data. An alternate service can be used in place of L\_ern\_ to make this data available to _Obsrv_ as well.
{% endhint %}

## Keycloak & Kong <a href="#sunbird-telemetry" id="sunbird-telemetry"></a>

\<description>

{% hint style="info" %}
Resolution :
{% endhint %}

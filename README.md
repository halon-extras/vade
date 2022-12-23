## Vade(host, opts)
Scans a message with Vade's Content Filter REST API.

**Params**

- host `string` - IP or hostname to the Vade service. **Required**.
- opts `array` - options array

**Returns**: class object.

The following options are available in the **opts** array.

- port `number` - TCP port. The default is 8080.
- timeout `number` - Timeout in seconds. The default is 10 seconds.
- tls `array` - TLS settings.
- max_message_size `number` - The max message size in bytes. The default is 5 MiB.

The following options are available in the **tls** array.

- enabled `boolean` - Enable TLS for the specific socket
- opts `array` - All available options can be found on [here](http://docs.halon.se/hsl/functions.html?highlight=tlssocket#TLSSocket)

## scan(fp, senderip, senderhelo, sender, recipients)

Scans a message

**Params**

- fp `File` - file object such as return type of [toFile()](https://docs.halon.io/hsl/functions.html#MailMessage.toFile). **Required**.
- senderip `string` - IP-address of the sender
- senderhelo `string` - The HELO of the sender
- sender `string` - The envelope sender
- recipients `array` - The [pre-defined](https://docs.halon.io/hsl/eodonce.html#transaction) `$transaction["recipients"]` object

**Returns**: associative array containing the result of the scan

**Return type**: `array`, when an error occur the "error" index is available.

## ping()

Pings the Vade's service to check if it's responding

**Returns**: `boolean`

## Example

```
include "vade";

$vade = Vade("172.16.78.25", ["port" => 8080, "tls" => ["enabled" => true]]);
$fp = $arguments["mail"]->toFile();
$result = $vade->scan($fp, $connection["remoteip"], $connection["helo"]["host"], $transaction["sender"], $transaction["recipients"]);

if (!$result["error"]) {
    echo $result;
} else {
    echo "Error - ".$result["error"];
}
```

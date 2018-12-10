# Donate if you want
https://www.paypal.me/compilenix

# Description
Geather detailed information on the TLS / SSL configuration of a given server.

# Dependencies
- Node.JS v8 or v9

# Supports
- IPv6
- unicode dns names like `plan-österreich.org`
- servers with multiple IPv4 and / or IPv6 addresses
- timeout (per connection)
- [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication) (Server Name Indication)
- ES6 async / await
- automatic `toString()` and `inspect()` formating for more readable console and debiggng output of result data

# Usage
__Note__: SNI is enabled and uses the value of the `host` option by default. To disable SNI set the option `servername` to `null`.

```js
const { TlsServiceAudit } = require('tlsinfo')

const tlsServiceAuditTask = new TlsServiceAudit({
  host: task.host,
  port: task.port,
  // servername: null, // optional to set or disable SNI
})
const result = await tlsServiceAuditTask.run()
```

All options which can be defined in the constructor of `TlsServiceAudit`, `Certificate`, `ProtocolVersion`, `Cipher` and `TlsSocketWrapper`: [github.com -> DefinitelyTyped -> node -> index.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/28a8ad8439307f87bcd8e5d12e50fe1e849ed82f/types/node/v9/index.d.ts#L5535).

The result is a object defined as [TlsServiceAuditResult](https://git.compilenix.org/Compilenix/types/blob/525275ec07db09709f07586913d4a1cd8b7e8dfe/tlsinfo/index.d.ts#L549).
Here is a example result as a json object: [compilenix.org/cdn/tlsinfo-example-audit-result.json](https://compilenix.org/cdn/tlsinfo-example-audit-result.json)\
__Note__: The unsupported list holds items that this lib can't test (because the Node.JS version does not support this particular ssl / tls / cipher combination).

If you only want to get the certificate/s you can use:
```js
const { Certificate } = require('tlsinfo')

const certificate = new Certificate({
  host: task.host,
  port: task.port
})
const result = await certificate.fetch()
```

The same applies to protocols (TLS 1.0, 1.1 etc.) -> `ProtocolVersion` and ciphers (AES128-GCM-SHA256, DHE-RSA-AES128-SHA256 etc.) -> `Cipher`.

Heavily inspired by [sslinfo](https://www.npmjs.com/package/sslinfo).

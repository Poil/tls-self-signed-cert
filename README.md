# TLS Self Signed Cert Terraform Module

- Generates a secure RSA or ECDAS private key for the CA cert
- Generates a self signed CA cert
- Generates a secure RSA or ECDAS private key for the leaf cert
- Generates a TLS certificate request for the leaf cert
- Generates a locally signed leaf cert
- Encodes the private keys as PEM

Checkout [examples](./examples) for fully functioning examples.

## Environment Variables

This module doesn't require any environment variables to be set.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| algorithm | The name of the algorithm to use for the key. Currently-supported values are "RSA" and "ECDSA". Defaults to "RSA". | `string` | `"RSA"` | no |
| allowed\_uses | List of keywords from RFC5280 describing a use that is permitted for the issued certificate. For more info and the list of keywords, see https://www.terraform.io/docs/providers/tls/r/self_signed_cert.html#allowed_uses. | `list` | <pre>[<br>  "key_encipherment",<br>  "digital_signature"<br>]</pre> | no |
| ca\_allowed\_uses | List of keywords from RFC5280 describing a use that is permitted for the CA certificate. For more info and the list of keywords, see https://www.terraform.io/docs/providers/tls/r/self_signed_cert.html#allowed_uses. | `list` | <pre>[<br>  "cert_signing",<br>  "key_encipherment",<br>  "digital_signature"<br>]</pre> | no |
| ca\_cert\_override | CA cert pem override. | `string` | `""` | no |
| ca\_common\_name | The common name to use in the subject of the CA certificate (e.g. hashicorp.com). | `string` | `""` | no |
| ca\_key\_override | CA private key pem override. | `string` | `""` | no |
| ca\_override | Don't create a CA cert, override with the provided CA to sign certs with. | `bool` | `false` | no |
| common\_name | The common name to use in the subject of the certificate (e.g. hashicorp.com). | `any` | n/a | yes |
| create | Create Module, defaults to true. | `bool` | `true` | no |
| dns\_names | List of DNS names for which the certificate will be valid (e.g. foo.hashicorp.com), defaults to empty list. | `list` | `[]` | no |
| download\_certs | Download certs locally, defaults to false. | `bool` | `false` | no |
| ecdsa\_curve | When algorithm is "ECDSA", the name of the elliptic curve to use. May be any one of "P224", "P256", "P384" or "P521". Defaults to "P224" | `string` | `"P256"` | no |
| ip\_addresses | List of IP addresses for which the certificate will be valid (e.g. 127.0.0.1), defaults to empty list. | `list` | `[]` | no |
| name | Filename to write the certificate data to, default to "tls-self-signed-cert". | `string` | `"tls-self-signed-cert"` | no |
| organization\_name | The name of the organization to associate with the certificates (e.g. HashiCorp Inc). | `any` | n/a | yes |
| permissions | The Unix file permission to assign to the cert files (e.g. 0600). Defaults to "0600". | `string` | `"0600"` | no |
| rsa\_bits | When algorithm is "RSA", the size of the generated RSA key in bits. Defaults to "2048". | `string` | `"2048"` | no |
| validity\_period\_hours | The number of hours after initial issuing that the certificate will become invalid. | `any` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| algorithm | The algorithm that was selected for the key. |
| ca\_cert\_filename | The CA cert filename. |
| ca\_cert\_name | The CA cert name. |
| ca\_cert\_pem | The CA cert data in PEM format. |
| ca\_cert\_validity\_end\_time | The time until which the CA certificate is invalid, as an RFC3339 timestamp. |
| ca\_cert\_validity\_start\_time | The time after which the CA certificate is valid, as an RFC3339 timestamp. |
| ca\_private\_key\_pem | The CA cert private key data in PEM format. |
| ca\_public\_key\_openssh | The CA cert public key data in OpenSSH authorized\_keys format, if the selected private key format is compatible. All RSA keys are supported, and ECDSA keys with curves "P256", "P384" and "P251" are supported. This attribute is empty if an incompatible ECDSA curve is selected. |
| ca\_public\_key\_pem | The CA cert public key data in PEM format. |
| leaf\_cert\_filename | The Leaf cert filename with file extension. |
| leaf\_cert\_name | The Leaf cert name. |
| leaf\_cert\_pem | The Leaf cert data in PEM format. |
| leaf\_cert\_request\_pem | The Leaf cert request data in PEM format. |
| leaf\_cert\_validity\_end\_time | The time until which the leaf certificate is invalid, as an RFC3339 timestamp. |
| leaf\_cert\_validity\_start\_time | The time after which the leaf certificate is valid, as an RFC3339 timestamp. |
| leaf\_private\_key\_filename | The Leaf cert private key filename with file extension. |
| leaf\_private\_key\_pem | The Leaf cert private key data in PEM format. |
| leaf\_public\_key\_openssh | The Leaf cert public key data in OpenSSH authorized\_keys format, if the selected private key format is compatible. All RSA keys are supported, and ECDSA keys with curves "P256", "P384" and "P251" are supported. This attribute is empty if an incompatible ECDSA curve is selected. |
| leaf\_public\_key\_pem | The Leaf cert public key data in PEM format. |

## Submodules

This module has no submodules.

## Authors

HashiCorp Solutions Engineering Team.

## License

Mozilla Public License Version 2.0. See LICENSE for full details.

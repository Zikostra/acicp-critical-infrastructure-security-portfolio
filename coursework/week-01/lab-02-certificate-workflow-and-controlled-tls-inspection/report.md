# ACICP201 Week 1 Lab 02

## Certificate Workflow and Controlled TLS Inspection

**Student:** Praise Nze
**Registration Number:** C11/26/ACIS/17358
**Course:** ACICP201 – Network Security Engineering

## Objective

The objective was to create a private certificate authority, issue a server certificate to VM-B, validate the TLS service from VM-A and capture the authorised TLS traffic.

## Laboratory Environment

| System | IP Address | Purpose |
|---|---|---|
| VM-A | 192.168.56.10 | TLS client and packet capture |
| VM-B | 192.168.56.20 | Private CA and TLS server |

All testing was restricted to the isolated laboratory network.

## Results

A private root CA named `ACICP201 Lab Root CA` was created successfully.

A server certificate was issued for VM-B with:

- Common Name: `acicp201-target`
- DNS SAN: `acicp201-target`
- IP SAN: `192.168.56.20`

Certificate-chain verification returned:

`server/target.crt: OK`

VM-A successfully validated the TLS service:

- `Verification: OK`
- `Verify return code: 0 (ok)`
- Certificate IP address matched `192.168.56.20`
- `SSL certificate verify ok`
- `HTTP/1.0 200 ok`
- Curl exit code: `0`

## Packet Capture

**PCAP filename:** `tls_test_8443.pcap`

**SHA-256:**

`a0996dbc9fe23a965c4fb0867dd27e0d25a34b1f24214d5871f5d7cbfa51a48f`

The capture contained authorised TLS traffic between VM-A and VM-B on TCP port 8443.

## Security-Control Explanation

### Role of the private CA

The private CA acted as the trusted authority that signed the VM-B server certificate. This allowed VM-A to verify that the certificate came from the authorised laboratory CA.

### Certificate fields proving the server identity

The Subject Alternative Name contained `IP Address:192.168.56.20`. The certificate also contained `DNS:acicp201-target` and was signed by the ACICP201 Lab Root CA.

### Information visible in encrypted TLS traffic

The packet capture still showed source and destination IP addresses, ports, timestamps, TCP flags, packet sizes and TLS handshake traffic. The encrypted application content was not visible.

### Why TLS decryption must be controlled

TLS decryption may expose passwords, personal information, confidential communications and operational data. It must therefore be authorised, documented and restricted.

### Traffic that should not be decrypted without approval

Banking, medical, legal, authentication, employee-private and regulated personal traffic should not be decrypted without explicit legal and organisational approval.

## Evidence

### Screenshots

1. `lab02-01-ca-certificate-creation.png`
2. `lab02-02-server-certificate-details.png`
3. `lab02-03-tls-server-running.png`
4. `lab02-04-vm-a-tls-validation.png`
5. `lab02-05-pcap-and-sha256.png`

### Text Evidence

1. `01_ca_and_server_certificate_creation.txt`
2. `04_vm_a_tls_validation_summary.txt`
3. `05_pcap_filename_sha256_and_summary.txt`

### Packet Capture

- `tls_test_8443.pcap`
- `tls_test_8443.sha256.txt`

## Conclusion

The private CA, server certificate, TLS service, certificate validation and controlled packet capture were completed successfully.

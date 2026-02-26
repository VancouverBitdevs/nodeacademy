We are going to generate an invoice with the following command. You can see below how we define the amount, a memo and an expiration time in seconds, which in this case is set to one month.

```shell
lncli addinvoice --memo "nodeacademy course objective" --amt 210000 --expiry 2592000
```

The relevant output will be the "payment request", and looks like this:

`lnbc2100u1p5v6mqapp5stqzsg053rk3afrw0uc59pd5y3tfe87n0dnjfshxnkhux8qkmmwqdpddehkgetpvdskgetd0ysxxmm4wfek2gr0vf4x2cm5d9mx2cqzzsxq9z0rgqsp5qcdr9awh0nnfat4hekh5ulx3laxcwgqdw7h2erc0pgp5d74j0x9q9qxpqysgqwlj7dcaeje5c3mxu6qeam8f8dtc8truguqqt4q3mpuqmx0mkyshphcyx3dmug729nuaml68n8nvzde05v7hy7875r6uns6nptu6afnspxs8d2m`

[[Useful LND Commands]]
]

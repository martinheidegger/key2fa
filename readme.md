---
theme: default
paginate: true
mdc: true
defaults:
  hideInToc: true
  layout: center
---

# Security Keys & WebAuthN

by Tillmann Weidinger [@Crabnebula](https://crabnebula.dev/)<br/>
and Martin Heidegger [@OWDDM](https://owddm.com)
<style>
footer {
  position: absolute;
  bottom: 2em;
  right: 2em;
}
</style>
<footer class="text-slate-300">
Kyoto, 2024/11/16
</footer>

---

# Todays Topics

<Toc />

---
hideInToc: false
---

# What are security keys?

---
hideInToc: false
---

![](./images/yubikeys-1024x417-515378429.jpg){width=400px lazy}

- Hardware Device
- Cost: between 4000円~25000円

---

<div class="flex flex-row items-center gap-9">

![](./images/Thetis_FIDO2_Security_Key_type_C.webp){width=300px lazy}

![](./images/fido-certified.png){width=100px lazy}

</div>

- Different makers
- Certified by a group

<!-- Make it yourself: https://www.wolfwithsword.com/hardware-diy-security-key/ -->

---

<div class="flex flex-row items-center gap-9">

![](./images/hid_Crescendo3000.jpg){width=300px lazy}

![](./images/vido-css-fingerprint-key.jpg){width=300px lazy}

</div>

- Different shapes
- Some with bio authenication

---

![](./images/makerdiary_key_internals.png){width=600px lazy}

- Simple hardware
- [Protocol](https://fidoalliance.org/specs/FDO/FIDO-Device-Onboard-PS-v1.1-20220419/FIDO-Device-Onboard-PS-v1.1-20220419.html) supports basic cryptographic primitives

---

## Crypto features

- Attestion

    _Verify that its made by a certified producer_

- Signatures

    _Create a signature for a data and offer a public key to verify it against._

- Encryption

    _Encrypt/Decrypt data. - not recommended._

---

#  When and where are they useful?

---
hideInToc: false
---

#  What is WebAuthN?

---
layout: full
---

![](./images/caniuse-webauthn.png)

---
layout: full
---

```ts {monaco-run}
const publicKeyCredentialCreationOptions = {
    challenge: Uint8Array.from(
        "UZSL85T9AFC", c => c.charCodeAt(0)),
    rp: {
        name: "Github Pages",
        id: "martinheidegger.github.io",
    },
    user: {
        id: Uint8Array.from(
            "UZSL85T9AFC", c => c.charCodeAt(0)),
        name: "lee@webauthn.guide",
        displayName: "Lee",
    },
    pubKeyCredParams: [{alg: -7, type: "public-key"}],
    authenticatorSelection: {
        authenticatorAttachment: "cross-platform",
    },
    timeout: 60000,
    attestation: "direct"
};
const credential = await navigator.credentials.create({
    publicKey: publicKeyCredentialCreationOptions
});
console.log(credential)
```

---
layout: iframe
url: https://martinheidegger.github.io/crypto-playground/index.html#/asymetric
---


---
hideInToc: false
---

#  What is the most common example for using security keys?

---
hideInToc: false
---

#  How can I use security keys to improve my work?

---

#  Q&A: Are security keys a useful technology?

---
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

```ts {monaco-run} {autorun:false}
const credential = await navigator.credentials.create({
    publicKey: {
      rp: { name: "Github Pages", id: "martinheidegger.github.io" },
      challenge: Uint8Array.from("UZSL85T9AFC", c => c.charCodeAt(0)),
      user: {
          id: Uint8Array.from("UZSL85T9AFC", c => c.charCodeAt(0)),
          name: "info@owddm.com",
          displayName: "OWDDM",
      },
      pubKeyCredParams: [{alg: -7, type: "public-key"}],
  }
});
console.log(credential)
```

---
layout: center
---

```ts
  rp: { name: "Github Pages", id: "martinheidegger.github.io" },
```

<v-clicks>

<div class="flex flex-row items-center gap-4 p-5 text-lg">
  <ruby>Public<rt>everyone can know this</rt></ruby>
  <ruby>Key<rt>binary data</rt></ruby>
  <ruby>Credential<rt>to verify</rt></ruby>
  <ruby>Rp <rt><em>of the</em> <abbr title="A Relying Party implementation typically consists of both some client-side script that invokes the Web Authentication API in the client, and a server-side component that executes the Relying Party operations and other application logic. Communication between the two components MUST use HTTPS or equivalent transport security, but is otherwise beyond the scope of this specification.">relying party</abbr></rt></ruby>
  <ruby>Entity<rt>(you can pass this around)</rt></ruby>
</div>

</v-clicks>

<v-clicks>

```ts
interface PublicKeyCredentialEntity {
    name: string;
}
interface PublicKeyCredentialRpEntity extends PublicKeyCredentialEntity {
    id?: string;
}
```

</v-clicks>
<v-clicks>

- `id` has to same as the **full** domain
- `name` is shown in the browser

</v-clicks>

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
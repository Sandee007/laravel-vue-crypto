# **laravel-vue-crypto**

### **This package integrates laravel's built in encryption service with vue**. It enables to encrypt/decrypt API data between laravel back-end and vue front-end. A typical usecase is when using laravel-inertia with axios.

<br>

## **This package requires the APP_KEY in .env passed in while initializing**

<br>

## **1. Install**

```
npm i laravel-vue-crypto
```

<br>

## **2. Setup**

### Inside **app.js**

<br>
Import the package :

```
import LaravelVueCrypto from 'laravel-vue-crypto'
```

<br>
Then register it as a vue-global-property

```
CONST APP_KEY = 'laravel-app-key' # .env's APP_KEY
app.config.globalProperties.$LaravelVueCrypto = new LaravelVueCrypto(APP_KEY)
```

<br>

## **3. Usage**

### **Encrypt data**

```
this.$LaravelVueCrypto.encrypt({'id': 1})
```

encrypt method always returns an object with attribute of payload. payload consists the encrypted string.

```
{payload : 'encrypted-string'}
```

### **Decrypt data**

```
this.$LaravelVueCrypto.decrypt(data)
```

<br>

## **Example**

```
const dataToEncrypt = {
    'id' : 1,
    'status' : 0
}

try {
    const res = await this.axios.post(
        route("test-route"),
        this.$LaravelVueCrypto.encrypt(dataToEncrypt)
    );

    decryptedData = this.$LaravelVueCrypto.decrypt(res?.data?.payload);
    console.log({ decryptedData });

} catch (err) {
    console.log({ err });
}
```
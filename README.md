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

```js
import LaravelVueCrypto from 'laravel-vue-crypto'
```

<br>
Then register it as a vue-global-property

```js
CONST APP_KEY = 'laravel-app-key' // laravel .env's APP_KEY
app.config.globalProperties.$LaravelVueCrypto = new LaravelVueCrypto(APP_KEY)
```

<br>

## **3. Usage**

### **Encrypt data**

```js
this.$LaravelVueCrypto.encrypt({'id': 1})
```

encrypt method always returns an object with attribute of payload. payload consists the encrypted string.

```js
{payload : 'encrypted-string'}
```

### **Decrypt data**

```js
this.$LaravelVueCrypto.decrypt(data)
```

<br>

## **Example**

### app.js
```js
createInertiaApp({
    setup({ el, App, props, plugin }) {
        const app = createApp({ render: () => h(App, props) })

        app.config.globalProperties.$LaravelVueCrypto = new LaravelVueCrypto(import.meta.env.VITE_APP_KEY)

        app.mount(el);
        return app;
    },
});
```


### .vue file
```js
const dataToEncrypt = {
    'id' : 1,
    'status' : 0
}

try {
    const res = await this.axios.post(
        route("test-route"),
        this.$LaravelVueCrypto.encrypt(dataToEncrypt)
    );

    const decryptedData = this.$LaravelVueCrypto.decrypt(res?.data?.payload);
    console.log({ decryptedData });

} catch (err) {
    console.log({ err });
}
```
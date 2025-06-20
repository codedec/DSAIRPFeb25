# Fast API and Streamlit

## Fast API

### Installing Requirements
```bash
# Install requirements
python -m pip install --upgrade pip
pip install "fastapi[standard]"
```

### Example 1: Simple String Message
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### Running Fast API
```bash
fastapi dev main.py
```

### Accessing Server
http://127.0.0.1:8000/

### Accessing Documentation
http://127.0.0.1:8000/docs



### Example 2: Simple JSON
```python
from fastapi import FastAPI
from typing import Union

app = FastAPI()


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q}
```

### Example 3: String Uppercase Conversion
```python
from fastapi import FastAPI
from typing import Union

app = FastAPI()

@app.get("/to_upper")
def to_upper(text: str):
    """Convert a query parameter 'text' to upper case."""
    return {"original": text, "upper": text.upper()}
```

### Example 4: Scikit-learn trained model serving
```python
from fastapi import FastAPI
from pydantic import BaseModel
import pickle
import numpy as np

app = FastAPI()

# Load the trained scikit-learn model
with open("lr_model.pkl", "rb") as f:
    model = pickle.load(f)


# Define the input schema
class ModelInput(BaseModel):
    feature1: float
    feature2: float
    feature3: float
    feature4: float


@app.post("/predict")
def predict(data: ModelInput):
    """Predict using the trained scikit-learn model."""
    features = np.array([[data.feature1, data.feature2, data.feature3, data.feature4]])
    prediction = model.predict(features)[0]
    return {"prediction": prediction}
```

## Streamlit
### How to run
```bash
streamlit run app.y

# OR
python -m streamlit run app.py

```

### Example 1 : Scikit-Learn Model Deployment
```python
import pickle
import streamlit as st
from os import path
import numpy as np


st.title("Flower Classification App")

file_name = "lr_model.pkl"
with open(path.join("model",file_name) , 'rb') as f:
    lr_model = pickle.load(f)

sl = st.number_input("Insert a sepel length")
sw = st.number_input("Insert a sepel width")
pl = st.number_input("Insert a petal length")
pw = st.number_input("Insert a petal width")

if st.button("Predict"):
    pred = lr_model.predict(np.array([[sl, sw, pl, pw]]))
    st.write("The flower is :", pred[0])
```



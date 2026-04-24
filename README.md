# Practical Task 6 — Deploy ML Model with FastAPI and Docker

## Project Structure
```
task6/
├── train.py          # Step 1: Train and save the model
├── main.py           # Step 2: FastAPI application
├── model.joblib      # Generated after running train.py
├── requirements.txt  # Dependencies
├── Dockerfile        # Step 4: Container instructions
└── README.md
```

---

## Step 1 — Train the Model
```bash
pip install -r requirements.txt
python train.py
```
Generates `model.joblib`.

---

## Step 2 & 3 — Run FastAPI Locally
```bash
uvicorn main:app --reload
```
- Root endpoint: http://localhost:8000/
- Predict endpoint: http://localhost:8000/predict
- Swagger docs: http://localhost:8000/docs

### Test /predict via curl:
```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"sepal_length":5.1,"sepal_width":3.5,"petal_length":1.4,"petal_width":0.2}'
```

---

## Step 4 & 5 — Build Docker Image
```bash
docker build -t iris-ml-api .
```

## Step 6 — Run the Container
```bash
docker run -p 8000:8000 iris-ml-api
```
Then test the same endpoints at http://localhost:8000

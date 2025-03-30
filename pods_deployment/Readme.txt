**Step 1: Create a Pod Using kubectl**

We will use the `tiangolo/uwsgi-nginx-flask` image, which comes pre-installed with Flask.

? **Run the following command to create a Pod:**

```
bash
kubectl run my-python-app --image=tiangolo/uwsgi-nginx-flask:python3.8 --restart=Never
```

? **Check if the Pod is running:**

```bash
kubectl get pods
```

? **Get details about the Pod:**

```bash
bash
kubectl describe pod my-python-app
```

---

## **2?? Step 2: Check Logs from the Pod**

? **View logs of the running Pod:**

```bash
bash
kubectl logs my-python-app
```

? **Follow real-time logs:**

```bash
bash
kubectl logs -f my-python-app
```

?? If the Pod crashes, check the previous logs:

```bash
bash
kubectl logs --previous my-python-app
```

---

## **3?? Step 3: Delete and Restart the Pod**

? **Delete the Pod:**

```bash
bash
kubectl delete pod my-python-app
```

? **Recreate the Pod using YAML.**

---

## **4?? Step 4: Create a Pod Using YAML**

Now, let’s create a **YAML file** to define our Pod.

?? **Create a file named `python-pod.yaml` and add the following content:**

```yaml
yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-python-app
  labels:
    app: python-web
spec:
  containers:
  - name: python-container
    image: tiangolo/uwsgi-nginx-flask:python3.8
    ports:
    - containerPort: 80

```

? **Apply the YAML file to create the Pod:**

```bash
bash
kubectl apply -f python-pod.yaml
```

? **Check the Pod Status:**

```bash
bash
kubectl get pods
```

? **Expose the Pod as a service to access it from the browser:**

```bash
bash
kubectl expose pod my-python-app --type=NodePort --port=80
```

? **Get the assigned NodePort:**

```bash
bash
kubectl get svc
```

? **Access the Web App:**

```bash
bash
curl http://<NODE_IP>:<NODE_PORT>
```

### **Project: Deploying a Simple Python Web Server Pod**

We will create a Pod running a **Python Flask app** that serves a simple webpage.

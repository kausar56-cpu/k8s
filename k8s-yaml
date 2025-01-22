rolling update at time all pod will update


apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: testpod1
  name: testpod1
spec:
  replicas: 6
  strategy:
    rollingUpdate:
      maxSurge: 100%
      maxUnavailable: 0
  selector:
    matchLabels:
      app: testpod1
  template:
    metadata:
      labels:
        app: testpod1
    spec:
      containers:
      - image: kiran2361993/kubegame:v2
        name: kubegame

rolling update at time all pod will not update after 10 sec 

  
apiVersion: apps/v1
kind: DeamonSet
metadata:
  labels:
    app: testpod1
  name: testpodi
spec:
  minReadySeconds: 10
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: testpod1  # This matches the labels in `template.metadata.labels`
  template:
    metadata:
      labels:
        app: testpod1  # This matches the `selector.matchLabels`
    spec:
      containers:
      - image: kiran2361993/kubegame:v2
        name: kubegame



demonset

kind: DeamonSet
metadata:
  labels:
    app: testpod1
  name: testpodi
spec:
  selector:
    matchLabels:
      app: testpod1  # This matches the labels in `template.metadata.labels`
  template:
    metadata:
      labels:
        app: testpod1  # This matches the `selector.matchLabels`
    spec:
      containers:
      - image: kiran2361993/kubegame:v2
        name: kubegame





db deploy


kind: Deployment
metadata:
  labels:
    app: testpod1
  name: testpod1
  annotations:
    info: "saikiran deployment"
    email: "saikiranpi"
    owner: "saikiranoi"
spec:
  replicas: 6
  selector:
    matchLabels:
      app: testpod1
  strategy: {}
  template:
    metadata:
      labels:
        app: testpod1
    spec:
      containers:
      - image: kiran2361993/kubegame:v2
        name: kubegame
        name:mysqldb
        env:
        - name: DB_NAME
          value: "mysqldb"
        - name: DB_PORT
          value: "3306"
        - name: DB_URL
          value: "saikiranpi.in/mydb"



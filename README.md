3️⃣ Build and Deploy in OpenShift
🏗️ Step 1: Build the image
oc new-build --strategy=docker --binary --name=simple-webapp
oc start-build simple-webapp --from-dir=. --follow

🧱 Step 2: Apply configs
oc apply -f openshift/configmap.yaml
oc apply -f openshift/secret.yaml
oc apply -f openshift/postgres.yaml
oc apply -f openshift/webapp.yaml

🗄️ Step 3: Initialize database
oc cp init_db.sql postgres-<pod-name>:/tmp/init_db.sql
oc rsh postgres-<pod-name> psql -U postgres -d testdb -f /tmp/init_db.sql

🌐 Step 4: Get route URL
oc get route simple-webapp -o jsonpath='{.spec.host}'

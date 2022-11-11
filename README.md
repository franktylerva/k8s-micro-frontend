This project demonstrates an approach to having separate, versioned frontend projects merged into one kubernetes pod via init containers.  Each init container should copy it's part of the application into a directory called shared-data.  This directory is mapped to a directory that is mounted by the nginx container for serving up the applications.  This example separates the application by feature, but one could use any technique to separate projects that makes sense.  Each feature is served up by nginx on a path that represents he feature.  So /feature-a for feature-a and /feature-d for feature-b.  Features in this project can be added via the helm charts values file under the key features.  The helm chart is located under the helm directory.  Execute the following command to install the example:
```
helm upgrade micro-frontend helm --install
```

Run the following commands to build feature-a:
```
cd feature-a
export PUBLIC_URL=/feature-a
yarn build
docker build -t feature-a:1.0.0 .
```

Run the following commands to build feature-b:
```
cd feature-b
export PUBLIC_URL=/feature-b
yarn build
docker build -t feature-b:1.0.0 .
```
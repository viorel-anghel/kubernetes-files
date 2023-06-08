
A simple kustomize example. 

NOTES:
- do not define namespaces in base files


Running

```
    kustomize build overlays/dev
# or
    kustomize build overlays/prod
```

will show the resulting yaml manifests.

To use kubectl directly, the syntax is something like:
```
    kubectl apply -k overlays/dev --dry-run=client -o yaml  # show only
# or
    kubectl apply -k overlays/dev  # really apply
```


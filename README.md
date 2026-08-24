# public

托管静态服务
kubectl -n novoai get pod deepcoach-backend-679d7c866f-l46ml -o yaml | grep -iE 'azure|workload|AZURE\_|serviceAccount'

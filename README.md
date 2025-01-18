 kubectl delete -f deployment.yml
  166  kubectl get all -n nginx
  167  kubectl apply -f deployment.yml
  168  kubectl get all -n nginx
  169  kubectl get logs mydeployment-54b9c68f67-2h695
  170  kubectl get logs pod/mydeployment-54b9c68f67-2h695
  171  kubectl get logs pod/mydeployment-54b9c68f67-2h695 -n nginx
  172  kubectl logs pod/mydeployment-54b9c68f67-2h695 -n nginx
  173  kubectl describe pod/mydeployment-54b9c68f67-2h695 -n nginx
  174  curl -f http://10.244.3.3
  175  curl -f http://10.244.3.3:80
  176  kubectl describe pod/mydeployment-54b9c68f67-2h695 -n nginx
  177  kubectl logs pod/mydeployment-54b9c68f67-2h695 -n nginx
  178  curl -f http://localhost:80
  179  nano deployment.yml
  180  kubectl get pods -n nginx
  181  kubectl exec -it mydeployment-54b9c68f67-2h695 -- bash
  182  kubectl exec -it mydeployment-54b9c68f67-2h695 -- bash -n nginx
  183  kubectl exec -it mydeployment-54b9c68f67-2h695 bash -n nginx
  184  ls
  185  nano service.yml
  186  nano deployment.yml
  187  ls
  188  kubectl get all -n nginx
  189  kubectl apply -f service.yml
  190  kubectl get all -n nginx
  191  curl -f http://localhost:80
  192  kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0:80
  193  kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0
  194  sudo -E kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0
  195  sudo -E kubectl port-forward service/nginx-service -n nginx 81:80 --address=0.0.0.0
  196  kubectl get all -n nginx
  197  kubectl describe service/nginx-service -n nginx
  198  ls
  199  kubectl delete all -n nginx
  200  kubectl delete all --all --force -n nginx
  201  kubectl get all -n nginx

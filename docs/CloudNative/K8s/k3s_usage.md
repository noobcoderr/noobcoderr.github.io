# K3S捣鼓使用记录

K3S捣鼓
1、跟随文档
	https://mp.weixin.qq.com/s/rTJ5ox5F75miAWx3t5jqUQ

2、遇到的问题
	1、执行kubectl get nodes时遇到WARN[0000] Unable to read /etc/rancher/k3s/k3s.yaml, please start server with --write-kubeconfig-mode to modify kube config permissions
		前面加sudo即可
	2、k3s搞不定，记录下卸载的命令，防止遗留垃圾
		https://segmentfault.com/a/1190000041111973?utm_source=sf-similar-article
		multipass delete --all
		mac删除multipass：https://blog.csdn.net/u012911498/article/details/123132724


curl -sfL http://rancher-mirror.cnrancher.com/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn INSTALL_K3S_EXEC="--docker" INSTALL_K3S_VERSION=v1.19.13+k3s1 K3S_URL=https://172.31.32.102:6443 K3S_TOKEN=K101a8b265a3393b5a342a9088a8a730c9fe32d9ca13b3205c23fdb36d2a26b84a9::server:d328370e3030a5faeabc6225d39570f5 sh -



k3s kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/kubesphere-installer.yaml

k3s kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/cluster-configuration.yaml


k3s kubectl logs -n kubesphere-system $(sudo kubectl get pod -n kubesphere-system -l app=ks-install -o jsonpath='{.items[0].metadata.name}') -f


kubectl run testapp --image=ccr.ccs.tencentyun.com/k8s-tutorial/test-k8s:v1







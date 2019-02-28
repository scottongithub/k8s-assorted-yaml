# Assorted Kubernetes Manifests

A collection of Kubernetes manifests in YAML format, to be used a-la-carte, for reference or to cut/paste as desired. Included:

* An nginx app that serves its container-hostname in its default webpage, useful for analyzing traffic/load-balancer operation

* A FileBeat daemonset that collects and ships container/kubernetes logs to AWS ElasticSearch/Kibana

* An implementation of the Lobsters app from [Kelsey Hightower's exceptional talk at PuppetConf 2016](https://www.youtube.com/watch?v=HlAXp0-M6SY) with updated APIs and semantics

* A "standard" storage class for any apps here that reference it

## Notes

These have all been created/tested on AWS EKS, created from [this Terraform script](https://github.com/scottongithub/terraform-aws-eks-infrastructure). AWS ElasticSearch is required for FileBeat and the ElasticSearch location/credentials need to be entered into the FileBeat containers' environment variables, editable in the FileBeat daemonset manifest.

The Kubernetes user must be associated with an IAM role that allows creation/deletion of cloud infrastructure (EBS, loadbalancers, etc). In the case of the Terraform script above, the IAM user is authenticated to *both* the cluster (via aws-iam-authenticator running on build machine) and to AWS (via aws-auth ConfigMap placed inside of the kube-system namespace)

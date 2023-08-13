<h1>EKS-2048</h1>

<p>This project deploys the 2048 game on AWS using Amazon EKS.</p>

<h2>Prerequisites</h2>

<p>Make sure you have the following tools installed:</p>

<ul>
  <li><code>kubectl</code></li>
  <ul>
    <li>Linux: <code>curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"</code></li>
    <li>MacOS: <code>curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"</code></li>
    <li>Windows: <code>curl.exe -LO "https://dl.k8s.io/release/v1.27.4/bin/windows/amd64/kubectl.exe"</code></li>
  </ul>
  <li><code>eksctl</code></li>
  <p>View installation instructions: <a href="https://github.com/eksctl-io/eksctl/blob/main/README.md">eksctl GitHub</a></p>
  <li>AWS CLI</li>
  <p>View installation documents: <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html">AWS CLI Install Guide</a></p>
  <li>Helm</li>
  <ul>
    <li>Linux:</li>
  </ul>
  <pre>
    <code>
      curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
      chmod 700 get_helm.sh
      ./get_helm.sh
    </code>
  </pre>
  <p>View Helm installation guide: <a href="https://helm.sh/docs/intro/install/">Helm Install Guide</a></p>
</ul>

<h2>🛠️ Setup Steps:</h2>

<p>1. Configure AWS credentials and region:</p>
<pre><code>aws configure</code></pre>

<p>2. Create an EKS cluster:</p>
<pre><code>eksctl create cluster --name {clusterName} --region {region} --fargate</code></pre>

<p>3. Download kubeconfig file:</p>
<pre><code>aws eks update-kubeconfig --name {clusterName} --region {region}</code></pre>

<h2>Actual Deployment</h2>

<h3>1. Create Fargate Profile</h3>
<pre><code>eksctl create fargateprofile \
--cluster {clusterName} \
--region {region} \
--name {name} \
--namespace {namespace}</code></pre>

<h3>2. Deploy the Game 2048</h3>
<pre><code>kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml</code></pre>

<h3>3. Check Deployments</h3>
<pre><code>kubectl get pods -n {namespace}</code></pre>

<h3>4. Check Services</h3>
<pre><code>kubectl get svc -n {namespace}</code></pre>

<h3>5. Create Ingress</h3>
<pre><code>kubectl get ingress -n {namespace}</code></pre>

<h3>6. Establish Trust Relationship for OIDC</h3>
<pre><code>eksctl utils associate-iam-oidc-provider --cluster {clusterName} --approve</code></pre>

<h2>ALB Controller</h2>

<h3>1. Download IAM Policy</h3>
<pre><code>curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json</code></pre>

<p>Or download from my git file iam_policy.json</p>

<h3>2. Create IAM Policy</h3>
<pre><code>aws iam create-policy \
--policy-name {policyName} \
--policy-document file://iam_policy.json</code></pre>

<h3>3. Create IAM Role</h3>
<pre><code>eksctl create iamserviceaccount \
--cluster={your-aws-account-id}\
--namespace= kube-system\
--name= aws-load-balancer-controller \
--role-name {roleName} \
--attach-policy-arn=arn:aws:iam::{your-aws-account-id}:policy/{policyName} \
--approve</code></pre>

<p>If there is an error, try it again.</p>

<h3>Create Controller</h3>
<h4>1. Add Helm Repo</h4>
<pre><code>helm repo add eks https://aws.github.io/eks-charts
helm repo update eks</code></pre>

<h4>2. Install AWS Controller</h4>
<pre><code>helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system \
--set clusterName
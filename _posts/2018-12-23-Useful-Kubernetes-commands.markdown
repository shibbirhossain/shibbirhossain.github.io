---
layout: post
title:  "Useful Kubernets commands"
date:   2018-12-22 09:38:04 +1100
categories: [blog, tech]
tags: [Kubernets, hot]
comments: true
---
![k8s](/assets/k8s.svg){: .center-image }

Get all namespaces:
{% highlight ruby %}
kubectl get ns
#=> returns all the namespaces
{% endhighlight %}

Get all resources:
{% highlight ruby %}
kubectl get all
#=> returns all the resources under default namespace
kubectl get pods -n yourawesomenamespace
#=> returns all the resources under yourawesomenamespace
{% endhighlight %}


Get pods:
{% highlight ruby %}
kubectl get pods
#=> returns all the pods under default namespace
kubectl get pods -n yourawesomenamespace
#=> returns all the pods under yourawesomenamespace
{% endhighlight %}


K8s contexts:
{% highlight ruby %}
kubectl config get-contexts
#=> returns all the available clusters
kubectl config use-context yourawesomecontext
#=> switches to yourawesomecontext
kubectl config set-context yourawesomecontext --namespace=yourawesomenamespace
# modifies context to use yourawesomenamespace as default namespace
{% endhighlight %}


K8s port forward:
{% highlight ruby %}
kubectl port-forward podname-43cc3323f -n yourawesomenamespace 5000:5000
#=> here podname-43cc3323f is a sample pod name. Left side of the port number (5000)
#=> exposes local machine port number, right side port number belongs to podname-43cc3323f
{% endhighlight %}

k8s describe pods:
{% highlight ruby %}
kubectl describe pods podname-43cc3323f -n yourawesomenamespace
#=> here podname-43cc3323f is a sample pod name.
{% endhighlight %}

k8s pod logs:
{% highlight ruby %}
kubectl logs podname-43cc3323f -n yourawesomenamespace
#=> here podname-43cc3323f is a sample pod name.
{% endhighlight %}




<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://shibbirhossain-1.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            

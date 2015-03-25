# consul-plugins-hue

Recipes are not yet available on the Cloudbreak UI, thus if you’d like to try this HUE plugin, we suggest to use the [Cloudbreak Shell](https://github.com/sequenceiq/cloudbreak-shell). 

Clone the project from GitHub.

```
git clone https://github.com/ziombski/consul-plugins-hue.git
```

From Cloudbreak shell (after the usuall steps - use `hint`):

```
recipe add --file /consul-plugins-hue/hue-recipe.json
```

Alternatively you can use the `--url` parameter to create the Spark recipe.

```
recipe add --url https://raw.githubusercontent.com/ziombski/consul-plugins-hue/master/hue-recipe.json
```

For using your recipe you have to select it. (you can check your recipes with `recipe list` command)
```
recipe select --id RECIPE_ID
```
In case of your blueprint and credential have already been selected and the instance groups are configured (`instancegroup configure`), create your stack with `create stack` command. If your stack is ready, you are able to create your cluster:

```
cluster create --description "Cloudbreak provisoned cluster with Apache HUE"
```

Please put these configurations in your blueprints:
```
"configurations": [
    {
        "hive-site": {
            "javax.jdo.option.ConnectionUserName": "hive",
            "javax.jdo.option.ConnectionPassword": "hive"
        }
    },
    {
        "core-site": {
            "hadoop.proxyuser.hue.hosts": "*",
            "hadoop.proxyuser.hue.groups": "*"
        }
    },
    {
        "webhcat-site": {
            "webhcat.proxyuser.hue.hosts": "*",
            "webhcat.proxyuser.hue.groups": "*"
        }
    },
    {
        "oozie-site": {
            "oozie.service.ProxyUserService.proxyuser.hue.hosts": "*",
            "oozie.service.ProxyUserService.proxyuser.hue.groups": "*"
        }
    }
```




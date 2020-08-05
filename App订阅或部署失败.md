### App订阅或部署失败

App部署失败，主要有两种情况，一是App订阅失败，二是App部署失败。

#### App订阅失败  

有多种情况会导致App订阅失败，而App订阅失败，也较好排查，一般通过UI就可以看出。常见的主要有以下几种情况。

- 订阅号User订阅App失败  

    - 由于只有订阅号下的Admin用户及Gloabl Admin用户可以订阅App，订阅号下的User用户订阅App时，UI会提示如下错误
        
          
          ![subscription user](/image/subscription user.png)

    - 解决方法

      - 使用订阅号下的Admin用户订阅App（可通过SSO Portal查看订阅号下的Admin用户）

            ![subscribe admin](/image/subscribe admin.png)

      - 修改订阅号下的User为Admin用户，然后订阅App（企业账号Admin有权限修改）

        ![modify subscribe role](/image/modify subscribe role.png)

- 未付费用户且非内部用户订阅App失败

    - 此种情况，UI会提示如下错误

          ![ispaid=false](/image/ispaid=false.png)

    - 解决办法

      - 首先通过SSO Protal查看订阅号付费类型，如图

            ![ssodetail](/image/ssodetail.png)

      - 结合上一步，若Is Paid=No，Is Internal=No，则符合未付费用户且非内部用户订阅App失败这种情况，请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）进行订阅部署

- 付费用户，点数不足，导致订阅App失败

    - 此种情况，UI会提示如下错误

          ![ispaid=true, wp is not enough](/image/ispaid=true, wp is not enough.png)

    - 解决方法

        请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）增加点数，再进行订阅App。

- 空间不足，导致订阅App失败  

    - 此种情况，选择部署的workspace或namespace时，UI会提示如下错误

          ![resources is not enough](/image/resources is not enough.png)

    - 解决方法

      - 若购买的是Dedicated Cluster，请自行对工作空间进行扩容，操作手册请参考：https://docs.wise-paas.advantech.com/zh-CN/Guides_and_API_References/Cloud_Services/1589509684297039988/1589890089018143254/v1.0.0   

      - 若购买的General Workspace，目前请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）对General Workspace进行扩容（扩容相当于加购General Workspace，这部分需要收费）。后续会有UI界面支持用户自主对General Workspace扩容

- client token调用失败，导致订阅App失败  

    - client token失效，导致订阅App失败，常见的有如下两种情况

      - client token失效，调用listingsystem返回401，导致订阅App订阅失败，UI会提示如下错误

            ![clienttoken失效-listing](/image/clienttoken失效-listing.png)

      - client token失效，调用order返回401，导致App订阅失败，UI提示如下错误，此时UI返回500，通过F12可以查看seviceinstanceConfig Api调用结果

            ![clinettoken失效-order](/image/clinettoken失效-order.png)

    - 解决方法

        请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）解决。

- order出现异常，导致订阅App失败

    - 此种情况，UI会提示如下错误，通过F12可以查看seviceinstanceConfig Api调用结果

          ![createorder失败](/image/createorder失败.png)

    - 解决方法

        请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）解决。

- Crmid在marketplace不存在，导致订阅App失败

    - 此种情况，UI会提示如下错误

          ![crmid is not in mkp](/image/crmid is not in mkp.png)

    - 解决方法

        请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）解决。

- 该空间已订阅过同一App（未退订干净），导致订阅App失败

    - 此种情况，UI会提示如下错误

          ![app is subscribe](/image/app is subscribe.png)

    - 解决方法

        请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）解决。

注：除上述几点外，App订阅失败，请先打开F12，找到调用失败的Api，查看返回的response，是否是上述情况的一种，如若都不是，请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com），并说明订阅情况。

#### App部署失败

App订阅成功后，即catalog ui上已经提示如下图信息，等待5min左右，namespace仍然没有部署订阅的App，那么App可能已经部署失败了。App部署失败，需要去排查Catalog api及Appbuy api的log信息，才能得出App部署失败的确切原因。

    ![subscription success](/image/subscription success.png)

- appbuy部署失败常见的几种情况
  - 空间资源不够
  - DB serviceinstance已关联过该App
  - DB serviceinstance不存在
  - 该namespace已存在某些资源（之前删除不干净）
  - chart不存在
  - helm部署超时
  - 获取mp config失败

- 解决方法

  若App部署失败，请联系WISE-PaaS.SRE（WISE-PaaS.SRE@advantech.com）解决，并说明Appbuy订阅及部署情况。



# zhifudashi_android_demo
支付大师android_demo版本,是真正的个人免签约第三方h5支付通道聚合支付接口，云端免挂机监控，即时到账，支持小程序、网站二维码扫码收款。只需个人微信支付宝账号即可自动化收款，超稳定不漏单
# 支付大师 http://zfds.codecocoa.com
## 是真正的个人免签约第三方h5支付通道聚合支付接口，云端免挂机监控，即时到账，支持小程序、网站二维码扫码收款。只需个人微信支付宝账号即可自动化收款，超稳定不漏单

## 接口文档  http://paydocs.codecocoa.com


### 对接简单，异步回调，安全高效，不限行业


``` java
 // 创建订单
    public void createOrder(){
        Map<String,String>postmap =new HashMap<>();
        String uid = "xxxxxxxxxxxxxxx";// 商户号 在商户后台查看
        String order_id = "21210729023137U97661109";// 商户订单号
        String order_price = "1.00";// 支付金额
        String redirect_url = "https://xxxdomain/api/paySuccessNoticeTest";// 填写您的接收支付成功的异步通知地址
        String returnUrl = "";// 同步通知地址
        String order_type = "alipay";// 请求支付类型
        String extension = ""; // 附加参数
        String secretKey = "xxxxxxxxxxxxxxxx";//商户密钥APPKEY 在商户后台查看

        // sign 签名是order_id+order_price MD5加密之后 再次+secretKey 然后再次MD5
        MD5 md5 =new MD5();
        String sign = md5.getSignMd5WithSecretkey(order_id,order_price,secretKey);
        System.out.println(sign);
        // 接口地址请到商户后台或者文档中心进行查看
        String url = "http://zfds.codecocoa.com/ApiOrders/createorder"; //"http://zfds.codecocoa.com/ApiOrders/createorde";// 发起订单地址
        Map<String, String> paramMap = new HashMap<>();// post请求的参数
        paramMap.put("order_id", order_id);
        paramMap.put("order_price", order_price);
        paramMap.put("redirect_url", redirect_url);
        paramMap.put("returnUrl", returnUrl);
        paramMap.put("order_type", order_type);
        paramMap.put("extension", extension);
        paramMap.put("sign", sign);
        paramMap.put("order_name", "测试商品name");
        paramMap.put("uid", uid);
        String parameters=map2Json(paramMap);
        System.out.println("parameters=="+parameters);
// Android 4.0 之后不能在主线程中请求HTTP请求
        new Thread(new Runnable(){
            @Override
            public void run() {
                OkHttpClient client = new OkHttpClient();
                MediaType json = MediaType.parse("application/json; charset=utf-8");
                RequestBody requestBody = RequestBody.create(json, parameters);
                Request requestPost = new Request.Builder()
                        .url(url)
                        .post(requestBody)
                        .build();
                Response response = null;
                String result = null;
                try {
                    response = client.newCall(requestPost).execute();
                    if (response.body() != null) {
                        result = response.body().string();
                    }
                } catch (IOException e) {
                    Log.d("TAG", "getStackTrace: "+e.getStackTrace().toString());
                }

                Log.d("result", "result: "+result);
            }
        }).start();




    }

    public String map2Json(Map<String,String> map){
        String mapjson="";
        Iterator<Map.Entry<String, String>> entries = map.entrySet().iterator();
        while (entries.hasNext()) {
            Map.Entry<String, String> entry = entries.next();
            mapjson=mapjson+'"'+entry.getKey()+'"' + ":"+'"'+entry.getValue()+'"'+",";
        }
        int strlength=(int)mapjson.length();
        mapjson=mapjson.substring(0,(strlength-1));
        mapjson="{"+mapjson+"}";
        return mapjson;
    }

```

### 交流群：QQ：385468484

### 更多demo
php:   https://github.com/mailes/zhifudashi_php_demo  
ios: https://github.com/mailes/zhifudashi_ios_demo    
android: https://github.com/mailes/zhifudashi_android_demo   
java:https://github.com/mailes/zhifudashi_java_demo   



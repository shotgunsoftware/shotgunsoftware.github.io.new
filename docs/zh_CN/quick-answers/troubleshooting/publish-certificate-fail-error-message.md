---
layout: default
title: urlopen 错误 SSL CERTIFICATE_VERIFY_FAILED 证书验证失败(_ssl.c:726)
pagename: publish-certificate-fail-error-message
lang: zh_CN
---

# `[ERROR publish_creation] <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:726)>`

## 用例

在 Houdini 17.5 中开发数字资产工具时，我使用构建工具包应用执行一个挂钩，尝试注册已发布的文件。

该脚本将执行代码：

        args = {
            "tk": self.parent.tank,
            "context": self.parent.engine.context,
            "path": esto['operator'],
            "name": os.path.basename(esto['operator']),
            "version_number": 6,
            "published_file_type": "Library item",
        }
        print 'sgtk: ', sgtk.__file__
        sg_publish = sgtk.util.register_publish(**args)

已发布的文件已在 {% include product %} 中正确注册，但显示以下错误：

```
---------------------------------------------------------------------------
[ERROR publish_creation] <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:726)>
Traceback (most recent call last):
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank/util/shotgun/publish_creation.py", line 308, in register_publish
    tk.shotgun.upload_thumbnail(published_file_entity_type, entity.get("id"), no_thumb)
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank_vendor/shotgun_api3/shotgun.py", line 2173, in upload_thumbnail
    field_name="thumb_image", **kwargs)
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank_vendor/shotgun_api3/shotgun.py", line 2263, in upload
    tag_list, is_thumbnail)
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank_vendor/shotgun_api3/shotgun.py", line 2383, in _upload_to_sg
    result = self._send_form(url, params)
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank_vendor/shotgun_api3/shotgun.py", line 3806, in _send_form
    resp = opener.open(url, params)
  File "/opt/hfs17.5.173/python/lib/python2.7/urllib2.py", line 429, in open
    response = self._open(req, data)
  File "/opt/hfs17.5.173/python/lib/python2.7/urllib2.py", line 447, in _open
    '_open', req)
  File "/opt/hfs17.5.173/python/lib/python2.7/urllib2.py", line 407, in _call_chain
    result = func(*args)
  File "/opt/hfs17.5.173/python/lib/python2.7/urllib2.py", line 1241, in https_open
    context=self._context)
  File "/opt/hfs17.5.173/python/lib/python2.7/urllib2.py", line 1198, in do_open
    raise URLError(err)
URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:726)>
Traceback (most recent call last):
  File "/home/cvizcarra/ollinDev/PIGS_kDev/config/hooks/publish_digital_asset.py", line 66, in register_publishedfile
    description='Alembic nodes.')
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank/log.py", line 503, in wrapper
    response = func(*args, **kwargs)
  File "/home/cvizcarra/ollinDev/PIGS_kDev/install/core/python/tank/util/shotgun/publish_creation.py", line 323, in register_publish
    entity=entity
ShotgunPublishError: Unable to complete publishing because of the following error: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:726)>, although PublishedFile PIGS_libary_tool_hda_asasas_v017.hda (id: 114715
) was created.
---------------------------------------------------------------------------
```

## 导致错误的原因是什么？

缺少 `cacert.pem` 和指向该位置的所需环境变量 `SHOTGUN_API_CACERTS`。

## 如何修复

添加 `cacert.pem` 和指向该位置的环境变量 `SHOTGUN_API_CACERTS`。

[在社区中查看完整主题](https://community.shotgridsoftware.com/t/ssl-certificate-error-on-sgtk-util-regiter-publish/3291)。


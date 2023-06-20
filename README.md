# 修改 ocr_server.py 中的get_img
```python
def get_img(request, img_type='file', img_name='image'):
    if img_type == 'b64': #
        try:  # json str of multiple images
            dic = json.loads(request.get_data())
            print(dic)
            img_base64 = dic.get(img_name)
            if 'base64,' in img_base64:
                img_base64 = img_base64.split('base64,')[1]
            img = base64.b64decode(img_base64)
        except Exception as e:  # just base64 of single image
            pass
    else:
        img = request.files.get(img_name).read()
    return img
```

# 请求方法
```json
{"image":"data:image/png;base64,iVBORw0KG"}
```
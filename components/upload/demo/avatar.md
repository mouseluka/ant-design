---
order: 1
title:
  zh-CN: 用户头像
  en-US: Avatar
---

## zh-CN

点击上传用户头像，并使用 `beforeUpload` 限制用户上传的图片格式和大小。

> `beforeUpload` 的返回值可以是一个 Promise 以支持异步处理，如服务端校验等：[示例](http://react-component.github.io/upload/examples/beforeUpload.html)。

## en-US

Click to upload user's avatar, and validate size and format of picture with `beforeUpload`.

> The return value of function `beforeUpload` can be a Promise to check asynchronously. [demo](http://react-component.github.io/upload/examples/beforeUpload.html)

```jsx
import { Upload, message } from 'antd';
import { LoadingOutlined, PlusOutlined } from '@ant-design/icons';

class Avatar extends React.Component {
  state = {
    loading: false,
  };

  render() {
    const { loading } = this.state;

    const uploadButton = (
      <div>
        {loading ? <LoadingOutlined /> : <PlusOutlined />}
        <div>Upload test</div>
      </div>
    );

    return (
      <Upload.Dragger
        name="upload"
        multiple
        customRequest={(params) => () => {onCancel: () => alert('aga')}}
        uploadListWrapperRender={(uploadListNode, fileList) => (
            <div>
                {JSON.stringify(fileList.map(i => i.percent))}
                <hr/>
                {uploadListNode}
            </div>)
        }
        itemRender={(originNode,
                    file,
                    onRemove,
                    fileList) => (
            <div>
                <hr/>
{/*3 {onAbort.toString()}<hr/>*/}
{/*{JSON.stringify(fileList)}*/}
<hr/>

                retry
                cancel
                <hr/>
{file.name}
<button onClick={() => onRemove(file)}>Remove</button>
            </div>
        )}
      >
        {uploadButton}
      </Upload.Dragger>
    );
  }
}

ReactDOM.render(<Avatar />, mountNode);
```

```css
.avatar-uploader > .ant-upload {
  width: 128px;
  height: 128px;
}
```

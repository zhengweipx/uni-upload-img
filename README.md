# 图片选择器
### 图片选择器
组件名：zw-upload-img。
#### 使用方式
> 在==script==中引用

```
import zwUploadImg from '@/components/zw-upload-img/zw-upload-img.vue'
export default {
    components: {zwUploadImg}
}
```
> 用法

```
<zw-upload-img :title="图片(工作票)" :num="9" :dataList="dataList"></zw-upload-img>
```
> zw-upload-img 属性说明

|属性名 | 类型 | 默认值 | 说明|
| :---------: | :-----------: |:---:|---|
| title | String | 图片(选填,提供问题图片,总大小10M以下) | 标题 |
| num | Number | 9 | 可选择图片数量 |
| dataList | Array | [] | 存放图片路径数组 |
| @chooseImg="chooseImg" | function | - | 见下 |
| @close="close($event)" | function | - | 删除单个图片,close(msg) {this.dataList = msg;} |

> Tips
- @chooseImg 函数体

```
chooseImg() {
	//选择图片
	uni.chooseImage({
		sourceType: ['camera', 'album'],
		sizeType: ['compressed', 'original'],
		count: this.num - this.dataList.length,
		success: res => {
			this.dataList = this.dataList.concat(res.tempFilePaths);
			// #ifdef APP-PLUS
			this.upLoadImg1(); //上传，需自行写
			// #endif
		}
	});
}
```

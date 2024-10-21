# Vue Quill Editor

## 에디터 사용하면서 새로 알게 된 점
> 1. **저장할 때 에디터 내용의 타입의 기본이 `Delta` 타입이라서 `HTML 형 변환`을 해주어야 `String`으로 저장 가능합니다.**   
> 2. **수정 할 때 값이 HTML(String)인 상태에서 에디터의 ContentType을 지정해주어야 한다.**


## 1번 예제 코드
```javascript
const updateContent = (currentContent) => {
  const delta = currentContent; // Delta 형식 데이터
  const converter = new QuillDeltaToHtmlConverter(delta.ops); // Delta를 HTML로 변환하는 인스턴스 생성
  const htmlContent = converter.convert(); // 변환된 HTML 내용
  emit('update:value', htmlContent); // 변환된 HTML을 부모 컴포넌트로 전달
};
```
> 에디터에 현재 작성한 내용은 기본 Delta 타입이고   
> 서버단에서 content 를 String 으로 받고 있습니다.   
> 따라서 해당 코드와 같이 HTML 타입으로 변환 해주어야 JSON Parsing 에러가 나지않습니다.  
> 
> 또한, Quill의 Delta 포맷은 사용자에게 그대로 보여줄 수 없습니다.   
> 일반적으로 웹 페이지에서 사용자에게 내용을 보여줄 때는 HTML 형식이 필요하므로,   
> Delta를 HTML로 변환하여 렌더링해야 합니다.


## 2번 예제 코드
```vue
  <QuillEditor
  :modules="modules"
  toolbar="minimal"
  :content="props.modelValue"
  @update:content="updateContent"
  :contentType="'html'" // default "Delta"
  />
```
> 수정하기를 진행하는 도중, DB에서 불러온 데이터는 분명히 나오는데  
> 수정하기 폼에 에디터 안에 기존 글 내용이 안나오는 문제가 생겼었습니다.  
> 이유는 해당 에디터의 ContentType 이 기본 Delta 였기때문에   
> 제가 불러온 값은 HTML 이기에 나타나지 않는 것 이었습니다.  
> 따라서, **ContentType 을 지정해주어 해결하였습니다.**  
 

## 최종 전체 코드
```vue
<template>
  <QuillEditor
  :modules="modules"
  toolbar="minimal"
  :content="props.modelValue"
  @update:content="updateContent"
  :contentType="'html'"
  />
</template>
<script setup>
  import ImageUploader from 'quill-image-uploader';
  import { QuillDeltaToHtmlConverter } from 'quill-delta-to-html';

  const props = defineProps({
  modelValue: {
  type: String,
  default: ''
}
});
  const emit = defineEmits(['update:value']);

const updateContent = (currentContent) => {
  const delta = currentContent; // Delta 형식 데이터
  const converter = new QuillDeltaToHtmlConverter(delta.ops); // Delta를 HTML로 변환하는 인스턴스 생성
  const htmlContent = converter.convert(); // 변환된 HTML 내용
  emit('update:value', htmlContent); // 변환된 HTML을 부모 컴포넌트로 전달
};

  const modules = {
  name: 'imageUploader',
  module: ImageUploader
};
</script>

<style scoped></style>

```


# vue-input-file-validate
ファイルのバイナリ情報でファイルタイプチェックをするやつ
拡張子偽装しててもある程度安心！

[DEMO](https://mattune.github.io/vue-input-file-validate/)

## 導入方法
1. /src/components/vifv-input.vue を任意の場所に追加。

## 使用方法
```html
<vifvInput name="sample" checkType="png,jpg,gif" required @checkResult="getResult"/>
```

checkTypeに判定したい拡張子、@checkResultに実行したいメソッドを記入。

### オプション
```html
<vifvInput checkType="png,jpg,gif"/>
```
→checkTypeはカンマ区切りで複数してい可能。

```html
<vifvInput checkType="png,jpg,gif" required/>
```
→requiredは自由に選択可能。

```html
<vifvInput name="sample" checkType="png,jpg,gif" required @checkResult="getResult"/>
```
→@checkResultは親コンポーネントのメソッドを指定可能。空でも可。

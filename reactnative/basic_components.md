# 基本元件Basic Components

## View

創建 UI 最基本的組件，類似 div, 它支持 flexbox 佈局、風格、一些觸發處理，和可訪問性控制，它被設計成嵌套在其他視圖裡



## Text
一個用於顯示文本的React組件，並且它也支持嵌套、樣式，以及觸摸處理。

```javascript=1
// 錯誤的做法：會導致一個錯誤。 <View>下不能直接放一段文本。
<View>
  一些文本
</View>

// 正確的做法
<View>
  <Text>
    一些文本
  </Text>
</View>
```

[支援屬性](http://reactnative.cn/docs/0.31/text.html#content)

## TextInput
TextInput是一個允許用戶在應用中通過鍵盤輸入文本的基本組件。本組件的屬性提供了多種特性的配置，譬如自動完成、自動大小寫、佔位文字等等。

最簡單的用法就是丟一個TextInput到應用裡，然後訂閱它的onChangeText事件來讀取用戶的輸入。

```javascript=1
<TextInput
  style={{height: 40, borderColor: 'gray', width: 150}}
  onChangeText={(text) => this.setState({text})}
  value={this.state.text}
/>
```

[支援屬性](http://reactnative.cn/docs/0.31/textinput.html#content)

## 練習1: 使用 Component
加入一個 TextInput Component 的名稱欄位，輸入後讓畫面顯示 Hello, XXX

```javascript=1
render() {
  return (
    <View style={styles.container}>
      <TextInput
        style={{height: 40, borderColor: 'gray', borderWidth: 1}}
        onChangeText={(text) => this.setState({text})}
        value={this.state.text}        
      />
      <Text style={styles.welcome} onPress={this.onPress} >
        {`Hello, ${this.state.text}`}
      </Text> 
    </View>
  );
}
```

## TouchableOpacity
本元件用於封裝視圖，使其可以正確響應觸摸操作。當按下的時候，封裝的視圖的透明度會降低。這個過程並不會真正改變視圖層級，大部分情況下很容易添加到應用中而不會帶來一些奇怪的副作用，例如做成按鈕使用。

```javascript=1
<TouchableOpacity onPress={this._onPressButton}>
  <Image
    style={styles.button}
    source={require('image!myButton')}
  />
</TouchableOpacity>
```

[支援屬性](http://reactnative.cn/docs/0.31/touchableopacity.html#content)

## 練習2：BMI 計算
用兩個 TextInput 分別讓使用者輸入身高,、體重，輸入完成後按按鈕進行計算，用 Text 顯示 BMI 值

```javascript=1
constructor(props) {
  super(props)
  this.state = {
    height: "",
    weight: "",
    BMI: "",
  }
} 
onPress = () => {
  console.log('pressed');
  this.setState({
    BMI: this.state.weight/(this.state.height*this.state.height)
  })
}
render() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>
        身高(公尺)
      </Text>
      <TextInput
        style={{height: 40, borderColor: 'gray', width: 150}} 
        onChangeText={(text) => this.setState({weight :text})}
        value={this.state.text}
      ></TextInput>
      <Text style={styles.text}>
        體重(公斤)
      </Text>
      <TextInput
        style={{height: 40, borderColor: 'gray', width: 150}}
        onChangeText={(text) => this.setState({weight :text})}
        value={this.state.text}
      ></TextInput>
      <TouchableOpacity onPress={this.onPress}>
        <Text>
          button
        </Text>
      </TouchableOpacity>
      <Text style={styles.text}>
        你的BMI是:
        {this.state.BMI}
      </Text>
    </View>
  );
}
```

## Image
一個用於顯示多種不同類型圖片的React組件，包括網絡圖片、靜態資源、臨時的本地圖片、以及本地磁盤上的圖片（如相冊）等。

```javascript=1
<Image
  style={styles.icon}
  source={require('./icon.png')}
/>
```

[支援屬性](http://reactnative.cn/docs/0.31/image.html)

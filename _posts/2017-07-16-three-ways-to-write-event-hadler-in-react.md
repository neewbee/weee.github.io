---
layout:     post
title:      react 组件中的事件的this绑定与参数传递
date:       2017-07-16 
summary:    三种写法
categories: react this event arrow 
---




{% highlight javascript linenos %}
function ChildComonent({ onClick, item }) {
  return <li onClick={onClick}>{item}</li>;
}

export default class Demo extends Component {
  constructor(props) {
    super(props)
    this.test3 = this.test3.bind(this)
    this.test6 = () => {
      console.log(this.state.id)
    }
    this.state = {
      id : 1
    };
  }

  test1({item, index}) {
    console.log(this.state.id)
    console.log(item, fetch(index))
  }

  test2(e) {
    console.log(this.state.id)
    console.log(e.currentTarget.dataset.id)
  }
  test3() {
    console.log(this.state.id)
  }

  test4({ id }) {
    console.log(id)
  }

  test5 = () => {
    console.log(this.state.id)

  };

  render() {
    const array = ['child1', 'child2', 'child3'];
    return (
      <div className={styles.container}>

        // bind this & pass data
        <div onClick={this.test4.bind(this, {id:this.state.id})}>test4</div>

        // caveat:create new function every render
        <div data-id = {1} onClick={(e) => this.test2(e)}>test2</div>

        // better
        <div onClick={this.test3}>test3</div>

        // property initializer (not standardized)
        <div onClick={this.test5}>test5</div>

        <ul>
          // null
          <li onClick={this.test1}>test1</li>

          // pass down parameters
          { array.map((item, index) => <ChildComonent onClick={this.test1.bind(this, { item, index})} item={item} /> )}
        </ul>

      </div>
    );
  }
}
{% endhighlight %}

其中test6与test5经过babel编译后没有区别

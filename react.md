## react(类组件)

生命周期:
componentWillMount(渲染结束之前(react 16 之后已经废弃))
componentDidMount(渲染完成之后)
componentWillUpdate(nextProps,nextState)(数据更新之前(react 16 之后已经被废弃))
componentDidUpdate(prevProps, prevState)(数据更新之后(里面进行判断上一个值和当前值是否不一致,不一致才做一些动作))
shouldComponentUpdate(nextProps, nextState)(是否决定更新)
componentWillUnmount(销毁)
不常用:
componentWillReceiveProps(传入的 props 数据改变之后执行操作(react 16 之后已经废弃))

## react 虚拟标签(state)

: <Fragment/> (外部不想标签的时候使用)
:所有状态放在 state 里面,使用 setState(x:x) 改变状态

## 类组件父子传参

`传参`:在组件上传入要传入的参数(<Head fun={传入的参数}></Head>)
`接参`:在 Head 组件里面使用 this.props.fun 来接受参数(父子传参)

## 类组件子父传参

`传参`:在父组件里定义一个回调( handClick=(value)=> value)
把这个方法传入到子组件里(<Head fun={this.handClick}></Head>)
`接参`:在子组件里调用父组件传过来的方法(this.props.fun(value))就可以在父组件拿到 value

## 类组件兄弟传参

:父组件里有一个状态,有一个方法
:把方法传给其中一个子组件,把另一个状态穿个另一个子组件

## 类组件 ref

**import { createRef } from 'react'**
Ref = createRef()
把 this.Ref 放到 dom 元素上(<input ref={this.Ref}/>)

## 高阶组件

`高阶组件:`const Hoc = (WillComponent) => { render(return (<WillComponent x={x}/>)) }
`普通组件:`引入 Hoc 这个组件 最后普通组件抛出 export default Hoc(普通组件) 使用 this.props 接收这个 x 参数(函数组件里给函数里传形参 props)

## 传参(发布订阅,跨级传参)

`<跨级传参>:`
在要传参的组件里引入:
**import { createContext } from 'react'**
export const MyContext=createContext()抛出去
<MyContext.Provider value={{ id: this.state.id, shop: 2 }}>
把要传参的组件放进来
</MyContext.Provider>

在要接收的组件里引入传参的组件:
**import {MyContext} from '组件位置'**
<MyContext.Consumer>
{(value) => value}
</MyContext.Consumer>

`在函数组件里跨级传参`
在要传参的组件里引入:
**import { createContext } from 'react'**
export const MyContext=createContext()抛出去
<MyContext.Provider value={{ id: this.state.id, shop: 2 }}>
把要传参的组件放进来
</MyContext.Provider>

在要接收的组件里引入传参的组件:
**import {useContext} from 'react'**
**import {MyContext} from '组件位置'**
const context = useContext(MyContext)

`<发布订阅>:`
**import PubSub from 'pubsub-js'**
发布:PubSub.publish('send', { title: 'x' })
接收:PubSub.subscribe('send', (\_, data) => {data 就是发不过来的数据})(可以随意接收)

## 路由

`单词`
Routes 包裹 Route 标签
Route 路由
Link a 标签跳转路由
Navigate 路由重定向
useNavigate 跳转路由
useRoutes 使用路由表

`在 src 下创建路由表`
**import { lazy } from 'react'**
懒加载 const home=lazy(()=>import(/_webpackChunkName:'home'_/ '路径'))
**import { Navigate } from 'react-router-dom'**
const routes=[{path:'/first',element:<路径名字 />},{path:'/',element:<Navigate to='/first'/>}]

`在最上面的组件(index.js)里引入`
**import { BrowserRouter } from 'react-router-dom'**
<BrowserRouter>
<Suspense fallback={标签}>(懒加载)
<App />
</Suspense>
</BrowserRouter>

`把路由放在你想放的地方:`
**import { Routes, Route, Link, Navigate, useRoutes,useNavigate } from 'react-router-dom'**
const element=useRoutes(引入路由表的路径)
把 element 放在你想显示路由的地方

`二级路由`
**import { Outlet } from 'react-router-dom'**
把 Outlet 放到要显示的地方

`跳转路由`
const jump=useNavigate()
jump(跳转的路由)
jump(-1)返回上一级

`路由传参`
jump(`/first ? id=12312312312`)
接收:**import {useLocation} from react-router-dom**
const location=useLocation()

## 类组件

**import React, { useState, useEffect, useRef, useContext } from 'react'**
useState:const [flag,setFlag]=useState(true)
useEffect:useEffect(()=>{ return ()=>{销毁}},[flag])
useRef:const Ref=useRef()

## redux

创建 redux 文件:里面有 action,reducer,store 文件

`action`:
const action = (value) => {return {type: 'SHOP_TYPE',value: value}}export { action }

`reducer`:
const initState = {
value: ''
}
const reducer = (state = initState, action) => {

    switch (action.type) {
        case 'SHOP_TYPE':
            return Object.assign({}, state, action)
    default:
            return state
    }

}
export { reducer }

`store`:
**import { createStore } from 'redux'**
**import { reducer } from './reducer'**
const store = createStore(reducer)
export default store

`基础使用`
在要传参的组件里:
**import { action } from 'action 组件位置'**
**import store from 'store 组件位置'**
使用发送:store.dispatch(action(value))

在要接参的组件里:
**import store from 'store 组件位置'**
store.getState()可以获取到 redux 的数据

`进阶使用`

在最上面的组件
**import { Provider } from 'react-redux'**
**import store from 'store 组件位置'**
<Provider store={store}>

        <App />

</Provider>

在使用的组件里
**import { connect } from 'react-redux'**
const mapStateToProps = (state, ownProps) => {

    return {
        prop: state.prop
    }

}
this.props 可以获取

const mapDispatchToProps = (dispatch, ownProps) => {

    return {
        dispatch1: (action) => {
            dispatch(action)
        }
    }

}
export default connect(mapStateToProps, mapDispatchToProps)(Home)

this.props.dispatch1(action)

<script setup>
import { onMounted } from "vue";
// 引入three.js
import * as THREE from 'three';
// 引入轨道控制器扩展库OrbitControls.js
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
// 引入dat.gui.js的一个类GUI
import { GUI } from 'three/addons/libs/lil-gui.module.min.js';

/** ============================================
 * 第一步：创建3D场景和物体
 * ========================================== */
// 创建3D场景对象Scene
const scene = new THREE.Scene();

// 创建一个 长方体
// const geometry = new THREE.BoxGeometry(40, 60, 40)
// 创建一个 球体
// const geometry = new THREE.SphereGeometry(50, 50, 20)
// 创建一个 圆柱
// const geometry = new THREE.CylinderGeometry(20, 40, 60, 60)
// 创建一个 圆锥
// const geometry = new THREE.ConeGeometry(20, 60, 10)
// 创建一个 平面
// const geometry = new THREE.PlaneGeometry(50, 30)
// 创建一个 圆环
const geometry = new THREE.TorusGeometry(30, 10, 30, 50)
// 创建一个 环结
// const geometry = new THREE.TorusKnotGeometry(30, 10, 300, 300)
// 创建一个 八面体
// const geometry = new THREE.OctahedronGeometry(30)
// 创建一个 十二面体
// const geometry = new THREE.DodecahedronGeometry(40)

// 创建一个材质对象Material
// 基础材质
// const material = new THREE.MeshBasicMaterial({ color: '#007bff' })
// 光滑材质
/*const material = new THREE.MeshLambertMaterial({
  color: '#007bff',     // 设置材质颜色
  // transparent: true,    // 开启透明
  // opacity: 0.9,         // 设置透明度
})*/
// 标准材质
/*const material = new THREE.MeshStandardMaterial({
  color: '#007bff',     // 设置材质颜色
  metalness: 0.5,       // 金属度
  roughness: 0.5,       // 粗糙度
})*/
// 物理材质
// const material = new THREE.MeshPhysicalMaterial({ color: '#007bff' })
// 网格高光材质
const material = new THREE.MeshPhongMaterial({
  color: '#1399d3',
  shininess: 10,        // 高光部分的亮度，默认30
  specular: '#1fecff',  // 高光部分的颜色
})

// 创建网格模型对象
const mesh = new THREE.Mesh(geometry, material);
// 设置坐标，默认是坐标原点
mesh.position.set(50,50,50);
// 把网格模型mesh添加到三维场景scene中
scene.add(mesh);

/** ============================================
 * 第二步：透视投影相机
 * ========================================== */
// 实例化一个透视投影相机对象
// const camera = new THREE.PerspectiveCamera()
// 定义相机输出画布的尺寸（canvas画布尺寸）
const width = 800;  // 宽度
const height = 500; // 高度
// 30:视场角度, width / height:Canvas画布宽高比, 1:近裁截面, 3000：远裁截面
const camera = new THREE.PerspectiveCamera(30, width / height)
// 根据需要设置相机位置具体值
camera.position.set(200, 200, 200)
// 相机观察目标指向Three.js 3D空间中某个位置
// 指向坐标原点
// camera.lookAt(0, 0, 0)
// 指向mesh对应的位置
camera.lookAt(mesh.position)

// 光源
const pointLight = new THREE.PointLight(0xffffff, 1.0)
pointLight.intensity = 1.0    // 光照强度
pointLight.decay = 0.0        // 设置光源不随距离衰减
//点光源位置
pointLight.position.set(300, 200, 300)
// 点光源添加到场景中
scene.add(pointLight)

// AxesHelper：辅助观察的坐标系
const axesHelper = new THREE.AxesHelper(150)
scene.add(axesHelper)

/** ============================================
 * 第三步：渲染器
 * ========================================== */
// 创建渲染器对象
const renderer = new THREE.WebGL1Renderer({
  antialias: true,   // 抗锯齿
})
// 设置缩放比率
renderer.setPixelRatio(window.devicePixelRatio)
// 设置背景颜色
renderer.setClearColor('#f1f1f1', 1)
// 设置three.js渲染区域的尺寸
renderer.setSize(width, height)
// 执行渲染操作
renderer.render(scene, camera)
// console.log(renderer.domElement)

// 动画渲染循环
// const clock = new THREE.Clock()
const render = () => {
  {
    // const spt = clock.getDelta()*1000 // 毫秒
    // console.log('两帧渲染时间间隔(毫秒)',spt)
    // console.log('帧率FPS',1000/spt)
    renderer.render(scene, camera)  // 执行渲染操作
    mesh.rotateY(0.01)  // 每次绕y轴旋转0.01弧度
    requestAnimationFrame(render) // 请求再次执行渲染函数render，渲染下一帧
  }
}

// 设置相机控件轨道控制器OrbitControls
const controls = new OrbitControls(camera, renderer.domElement);
// 如果OrbitControls改变了相机参数，重新调用渲染器渲染三维场景
// 监听鼠标、键盘事件
controls.addEventListener('change', function () {
  // 执行渲染操作
  renderer.render(scene, camera)
})

// 实例化一个gui对象
const gui = new GUI();
//改变交互界面style属性
gui.domElement.style.right = '0px';
gui.domElement.style.width = '300px';
const obj = {
  x: 50,
  y: 50,
  z: 50,
};
// gui增加交互界面，用来改变obj对应属性
gui.add(obj, 'x', 0, 100);
gui.add(mesh.position, 'x', -1000, 1000);
gui.add(mesh.position, 'y', -1000, 1000);
gui.add(mesh.position, 'z', -1000, 1000);

// p1、p3轨迹线起始点坐标
const p1 = new THREE.Vector3(-100, 0, -100);
const p3 = new THREE.Vector3(100, 0, 100);
// 计算p1和p3的中点坐标
const x2 = (p1.x + p3.x)/2;
const z2 = (p1.z + p3.z)/2;
const h = 100;
const p2 = new THREE.Vector3(x2, h, z2);
// 三维二次贝赛尔曲线
const curve = new THREE.QuadraticBezierCurve3(p1, p2, p3);


onMounted(() => {
  document.getElementById('webgl').appendChild(renderer.domElement)
  render()
})

const btn = (e, data) => {
  console.log(e, data)
}

</script>

<template>
  three.js实例
  <div id="webgl"></div>
<!--  <button @click="btn($event, '1212')">按钮</button>-->
<!--  <button @click="e => btn(e, '1233')">按钮</button>-->
</template>

<style lang="scss" scoped>

</style>

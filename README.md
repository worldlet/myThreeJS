### 什么是 ThreeJS

ThreeJS 是一个用于创建和显示3D图形的JavaScript库。它建立在WebGL之上，提供了一个简化的API，使开发者能够更容易地在Web浏览器中创建复杂的3D场景。Three.js允许开发者使用JavaScript创建交互式的3D图形，而无需深入了解WebGL的复杂性。

主要特点包括：

>1. 跨平台： Three.js 可以在支持WebGL的各种平台上运行，包括 *桌面* 和 *移动设备*。
>2. 易用性： 提供了高级的、面向对象的API，简化了3D图形的创建和渲染。
>3. 性能： Three.js 通过优化和抽象底层WebGL，提供了更高层次的抽象，使开发者更容易利用WebGL的潜力而不必直接处理底层细节。
>4. 社区支持： Three.js有一个庞大的开发者社区，提供了大量的文档、示例和插件，使得学习和使用库变得更加容易。

使用Three.js，开发者可以创建各种各样的3D场景，包括游戏、数据可视化、教育应用等。通过结合HTML、CSS和JavaScript，它使得在Web浏览器中实现高性能的3D图形变得相对简单。

精彩实例：[threejs-journey](https://threejs-journey.com/) [3D案例](http://www.yanhuangxueyuan.com/3D.html)

### 如何学习ThreeJS

有没有原生WebGL基础，你都可以直接学习Three.js,刚刚入门three.js时候，可以先不用学习WebGL，当你需要进阶深入学习Three.js的时候，最好先去学学原生WebGL，了解了解图形学相关理论知识，即便只是稍微入门WebGL，那对于three.js深入学习帮助都是很大的。

关于WebGL的推荐书籍：
入门：《WebGL编程指南》
图形学：《交互式计算机图形学基于WebGL的自顶向下方法》

### VUE中引用ThreeJS

threejs知识点相对普通web前端是比较独立的，threejs的用法，你直接用.html文件写，还是结合vue或React框架写，API语法都是一样的。
所以学习threejs的重点不是考虑前端框架问题，而是threejs本身，掌握了threejs，剩下的事情就很简单了。

```js
// 比如安装157版本
npm install three@0.157.0 --save

// VUE中引用ThreeJS
import * as THREE from 'three';
// 引入扩展库OrbitControls.js
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
// 引入扩展库GLTFLoader.js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
```

其他引用方法：[链接](http://www.webgl3d.cn/pages/cd35b2/)

### 实现一个简单的案例

首先ThreeJS中有三个主要的概念：**场景Scene**、**相机Camera**、**渲染器Renderer**

![[Pasted image 20231128143732.png]]

场景 `Scene` 就相当于一个容器，包含了所有的三维对象，而相机 `Camera` 定义了观察场景的视角和投影方式（即用户的视角），渲染器 `Renderer` 负责将场景和相机中的3D元素渲染到屏幕上。

#### 三维场景 `Scene`

可以把三维场景Scene对象理解为虚拟的3D场景，用来表示模拟生活中的真实三维场景，或者说三维世界。

其中包含一些概念：
**物体形状** `几何体Geometry`：
BoxGeometry（立方体几何体）、SphereGeometry（球体几何体）、CylinderGeometry（圆柱几何体）、ConeGeometry（圆锥几何体）、PlaneGeometry（平面几何体）、TorusGeometry（圆环几何体）、TorusKnotGeometry（环结几何体）、OctahedronGeometry（八面体几何体）、DodecahedronGeometry（十二面体几何体）等等。
**物体外观** `材质Material`
基础材质（Basic Material）、光滑材质（Lambert Material）、标准材质（Standard Material）、物理材质（Physical Material）、标准表面反射材质（Standard Surface Reflectance Material）、Phong 材质、点云材质（Points Material）、线条材质（Line Material）、线段材质（Line Dashed Material）、Sprite 材质、自定义着色器材质（Shader Material）等等。
**物体** `网格模型Mesh`
Mesh 是一种用于创建网格模型的对象。网格模型是由几何体（Geometry 或 BufferGeometry）和材质（Material）组成的，它定义了物体的形状和外观。
**模型位置** `.position`
一个物体是有位置的，对于threejs而言也是一样，可以通过位置属性.position定义网格模型Mesh在三维场景Scene中的位置，包含了模型在三维空间中的坐标，包含了模型的 X、Y、Z 坐标值，分别代表模型在水平、垂直和深度方向上的位置。

```js
// 创建3D场景对象Scene
const scene = new THREE.Scene()

// 创建一个 长方体
const geometry = new THREE.BoxGeometry(40, 60, 40)
// 创建一个 球体
const geometry = new THREE.SphereGeometry(50, 50, 50)
// 创建一个 圆柱
const geometry = new THREE.CylinderGeometry(20, 40, 60, 60)
// 创建一个 圆锥  
const geometry = new THREE.ConeGeometry(20, 60, 10)

// 基础材质
const material = new THREE.MeshBasicMaterial({ color: '#007bff' })  
// 标准材质  
const material = new THREE.MeshStandardMaterial({  
  color: '#007bff',     // 设置材质颜色  
  metalness: 0.5,       // 金属度  
  roughness: 0.5,       // 粗糙度  
})
// 网格高光材质  
const material = new THREE.MeshPhongMaterial({  
  color: '#1399d3',  
  shininess: 10,        // 高光部分的亮度，默认30  
  specular: '#1fecff',  // 高光部分的颜色  
})

// 创建网格模型对象
const mesh = new THREE.Mesh(geometry, material)

// 设置坐标，默认是坐标原点  
mesh.position.set(50, 50, 50)

// 把网格模型mesh添加到三维场景scene中
scene.add(mesh); 
```

#### 相机 Camera`

Threejs提供了正投影相机 `OrthographicCamera` 和透视投影相机 `PerspectiveCamera` ，暂时先用常用的透视投影相机 `PerspectiveCamera`。
透视投影相机 `PerspectiveCamera` 本质上就是在模拟人眼观察这个世界的规律，也就是**相机就相当于用户的视角**。

其中包含一些概念：
**相机位置** `.position`：
相机的位置是通过 .position 属性来表示的。这个属性包含了相机在三维空间中的坐标。就像模型的位置一样，.position 属性包含了相机的 X、Y、Z 坐标值，分别代表相机在水平、垂直和深度方向上的位置。通过调整相机的位置，你可以改变观察场景的视角，实现不同的观察效果。相机的位置在渲染场景时至关重要，它决定了观察者的位置和方向，从而影响最终呈现在屏幕上的图像。
**相机观察目标** `.lookAt()`：
在 Three.js 中，.lookAt() 方法是相机对象的一个方法，用于设置相机的朝向或观察目标。通过这个方法，你可以让相机指向场景中的某个特定点或物体，从而改变相机的方向。.lookAt() 方法通常在渲染循环中被调用，以确保相机的朝向动画流畅地被更新。这对于创建动态的相机视角效果非常有用，特别是在用户交互和动画场景中。
**透视投影相机** `PerspectiveCamera`：**视锥体**
在 Three.js 中，透视投影相机（PerspectiveCamera）使用透视投影来模拟现实世界中的视觉效果。视锥体（frustum）是透视投影相机的一个概念，表示相机能够看到的空间范围。由四个参数fov（视野角度）, aspect（长宽比）, near（近平面距离）, far（远平面距离）构成一个四棱台3D空间，被称为视锥体，只有视锥体之内的物体，才会渲染出来，视锥体范围之外的物体不会显示在Canvas画布上。

![[Pasted image 20231128164019.png]]

```js
// 定义相机输出画布的尺寸，即canvas画布尺寸
const width = 800   // 宽度
const height = 500  // 高度
// fov视场角度：30, aspect画布宽高比：width / height, 近裁截面：1, 远裁截面：3000
const camera = new THREE.PerspectiveCamera(30, width / height, 1, 3000)
// 根据需要设置相机位置具体值  
camera.position.set(200, 200, 200)
// 相机指向创建的网格模型mesh对应的位置
camera.lookAt(mesh.position)
```

#### WebGL渲染器 `WebGLRenderer`

WebGLRenderer 是 Three.js 中的渲染器，用于将场景中的三维对象渲染到浏览器的画布上。它基于 WebGL 技术，利用 GPU 加速来实现高性能的三维渲染。通过WebGL渲染器 `WebGLRenderer` 可以实例化一个WebGL渲染器对象（也就是上面创建的网格模型mesh），然后呈现在浏览器上。

```js
// 创建渲染器对象
const renderer = new THREE.WebGL1Renderer({  
  antialias: true,   // 抗锯齿  
})
// 设置缩放比率  
renderer.setPixelRatio(window.devicePixelRatio)
// 设置背景颜色  
renderer.setClearColor('#ffffff', 1)
// 设置three.js渲染区域的尺寸  
renderer.setSize(width, height)  
// 执行渲染操作  
renderer.render(scene, camera)
// 可以通过renderer.domElement查看渲染的DOM节点为canvas标签
console.log(renderer.domElement)  // <canvas data-engine="three.js r157" width="1000" height="625" style="display: block; width: 800px; height: 500px;"></canvas>
```


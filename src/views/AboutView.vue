<template>
  <div class="container">
  </div>
</template>


<script>
//npm start
import * as THREE from 'three'
// import {RectAreaLightHelper} from 'three/examples/jsm/helpers/RectAreaLightHelper'
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls';
import * as dat from 'dat.gui'
import Stats from 'three/examples/jsm/libs/stats.module'
// import {FBXLoader} from 'three/examples/jsm/loaders/FBXLoader.js'


// const gui = new dat.GUI({autoPlace: false});
// container.appendChild(gui.domElement);

export default {
  name: 'AboutView',
  mounted(){
    const scene = new THREE.Scene();

    // scene.background = new THREE.Color(0xffff00);
    scene.background = new THREE.Color(0xDDDDDD);

    const camera = new THREE.PerspectiveCamera(
      20,
      (window.innerWidth - 20)/(window.innerHeight/2),
      0.1,
      1000
    );
    camera.position.x = 15
    camera.position.y = 15
    camera.position.z = 15
    camera.lookAt(0,0,0);
    scene.add(camera);
    
    // camera.fov = 46;
    camera.updateProjectionMatrix();
    // camera.zoom(2);


    ///////////////////////
    //FBX
    ///////////////////////
    // const loader = new FBXLoader();
    //   // loader.load("files/body.FBX", (obj) => {
    //   //   obj.scale.x = obj.scale.y = obj.scale.z = .0005;
    //   //   obj.position.x -= 15;
    //   //   obj.traverse(function(child){
    //   //       if(child.isMesh){
    //   //           child.castShadow = true;
    //   //           child.receiveShadow = true;
    //   //       }
    //   //   });
    //   //   scene.add(obj)
    //   // });

    //   loader.load("files/StaticMesh1.FBX", obj => {
    //               obj.scale.x = obj.scale.y = obj.scale.z = .5;
        
    //               obj.position.x = 10;
    //     obj.position.y = .5;
    //     obj.position.z = 2.6;

    //     obj.rotation.x = -90 * ( Math.PI / 180 ); 
    //     obj.rotation.z = -160 * ( Math.PI / 180 ); 
        
    //     scene.add(obj)
    //   })

    //   loader.load("files/StaticMesh2.FBX", obj => { // 3호기 집게 축
    //     obj.scale.x = obj.scale.y = obj.scale.z = .5;

    //     obj.position.x = 6.7;
    //     obj.position.y = -1.3;
    //     obj.position.z = 2.8;

    //     obj.rotation.x = -90 * ( Math.PI / 180 ); 
    //     obj.rotation.z = -10 * ( Math.PI / 180 ); 

    //     obj.traverse(function(child){
    //         if(child.isMesh){
    //             child.castShadow = true;
    //             child.receiveShadow = true;
    //         }
    //     });

    //     scene.add(obj)
    // });

    // loader.load("files/StaticMesh3.FBX", obj => { // 3호기 Y축
    //     obj.scale.x = obj.scale.y = obj.scale.z = .5;

    //     obj.position.x = 5;
    //     obj.position.z = 1.4;

    //     obj.rotation.x = -90 * ( Math.PI / 180 ); 
    //     obj.rotation.z = -170 * ( Math.PI / 180 ); 

    //     obj.traverse(function(child){
    //         if(child.isMesh){
    //             child.castShadow = true;
    //             child.receiveShadow = true;
    //         }
    //     });

    //     scene.add(obj)
    // });

    // loader.load("files/StaticMesh4.FBX", obj => { // 3호기 몸체
    //     obj.scale.x = obj.scale.y = obj.scale.z = .5;

    //     obj.position.x = 5;

    //     obj.rotation.x = -90 * ( Math.PI / 180 ); 
    //     obj.rotation.z = -170 * ( Math.PI / 180 ); 

    //     obj.traverse(function(child){
    //         if(child.isMesh){
    //             child.castShadow = true;
    //             child.receiveShadow = true;
    //         }
    //     });

    //     scene.add(obj)
    // });

    //////////////////////
    //container
    /////////////////////

    const renderer = new THREE.WebGLRenderer();
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth - 20, window.innerHeight / 2);
    renderer.shadowMap.enabled = true

    new OrbitControls(camera, renderer.domElement);   //good

    const container = document.querySelector('.container');   //컨테이너
    container.appendChild(renderer.domElement);

    const stats = new Stats();
    document.body.appendChild(stats.dom);

    const gui = new dat.GUI({autoPlace: false});
    container.appendChild(gui.domElement);
    gui.domElement.style.position="relative";
    gui.domElement.style.bottom=`${container.clientHeight}px`;
    gui.domElement.style.left=`${container.clientWidth-gui.domElement.clientWidth-4}px`;
    
    const axisFolder = gui.addFolder('axis');
    

    //////////////////////////
    //Light
    //////////////////////////

    // const ambientLight = new THREE.AmbientLight(0xff0000, 1); //빛의 색상/ 빛을 얼마나 세게
    // scene.add(ambientLight)
    
    // const directionalLight = new THREE.DirectionalLight(0xff0000, 1); //방향
    // directionalLight.position.x+=2
    // directionalLight.position.y+=2
    // directionalLight.position.z+=2
    // scene.add(directionalLight)

    // scene.add(new THREE.DirectionalLight(0xffffff, 0.2));
    // const PointLight = new THREE.PointLight(0xffff00, 1, 0.0, 0);
    // PointLight.position.y = 10
    // PointLight.decay=1.9
    // scene.add(PointLight);
    // scene.add(new THREE.PointLightHelper(PointLight))

    // const hemisphereLight = new THREE.HemisphereLight(0x0000ff, 0xff0000,1);
    // scene.add(hemisphereLight);

    // const rectareaLight = new THREE.RectAreaLight(0xffffff, 1, 3, 3);
    // rectareaLight.position.y += 3
    // scene.add(rectareaLight);
    // scene.add(new RectAreaLightHelper(rectareaLight))

    const light = new THREE.AmbientLight(0xffffff, 0.9);
    scene.add(light)

    const spotlight = new THREE.SpotLight(0xfd9629, 2, 14, 0.3, 1, 1)
    spotlight.position.y=10
    scene.add(spotlight)

    ///////////////////////////////////////////
    //meterial
    //////////////////////////////////////////
    const planeGeometry = new THREE.PlaneGeometry(15, 15)
    const planematerial = new THREE.MeshStandardMaterial({color: 0xffffff});
    const planeMesh = new THREE.Mesh(planeGeometry, planematerial);
    planeMesh.rotateX(- (Math.PI/2))
    scene.add(planeMesh)

    // const geometry = new THREE.BoxGeometry(1, 1, 1)
    // const meterial = new THREE.MeshStandardMaterial()
    // meterial.color.set(0xff0000)
    // const mesh = new THREE.Mesh(geometry, meterial)
    // mesh.position.set(0, 0, 0)
    // scene.add(mesh)
    
    // const geometry = new THREE.TorusGeometry(2, 2, 20, 20, Math.PI *2)
    // const meterial = new THREE.MeshBasicMaterial({ color: 0xffff00 })
    // const mesh = new THREE.Mesh(geometry, meterial)
    // mesh.position.set(0, 0, 0)
    // scene.add(mesh)
    
    // const geometry2 = new THREE.BoxGeometry(1, 1, 1)
    // const meterialstand = new THREE.MeshStandardMaterial()
    // meterialstand.color.set(0xff0000)
    // meterialstand.metalness = 0.5;
    // meterialstand.transparent = true;
    // meterialstand.opacity=0.6;
    // const mesh2 = new THREE.Mesh(geometry2, meterialstand)
    // mesh2.position.x += 2
    // mesh2.position.z += 2
    // scene.add(mesh2)

    // const geometry2 = new THREE.TorusGeometry(0.75, 0.3, 20, 20, Math.PI *2)
    // const meterialstand = new THREE.MeshPhysicalMaterial()
    // meterialstand.color.set(0xaa0000)
    // meterialstand.clearcoat = 1;
    // const mesh2 = new THREE.Mesh(geometry2, meterialstand)
    // mesh2.position.x += 2
    // mesh2.position.y += 2
    // mesh2.position.z += 2
    // scene.add(mesh2)

    // const geometry2 = new THREE.TorusGeometry(0.75, 0.3, 20, 20, Math.PI *2)
    // const meterialstand = new THREE.MeshLambertMaterial()
    // meterialstand.color.set(0xaa0000)
    // const mesh2 = new THREE.Mesh(geometry2, meterialstand)
    // mesh2.position.x += 2
    // mesh2.position.y += 2
    // mesh2.position.z += 2
    // scene.add(mesh2)

    const geometry2 = new THREE.TorusGeometry(0.75, 0.3, 20, 20, Math.PI*2)  //크기, 안에 빈공간, 얼마나 쪼개나, 안을 얼마나 쪼개나, 얼마나 그릴지
    const meterialstand = new THREE.MeshPhongMaterial()
    meterialstand.color.set(0x777700)
    meterialstand.shininess=120   //디폴트가 30
    meterialstand.specular.set(0xffff00)
    const meshh = new THREE.Mesh(geometry2, meterialstand)
    meshh.position.y += 1
    scene.add(meshh)

    // const geometry2 = new THREE.TorusGeometry(0.75, 0.3, 20, 20, Math.PI *2)
    // const meterialstand = new THREE.MeshToonMaterial()
    // meterialstand.color.set(0x770000)
    // const mesh2 = new THREE.Mesh(geometry2, meterialstand)
    // mesh2.position.y += 2
    // scene.add(mesh2)

    ///////////////////////////
    //geometry
    ///////////////////////////
    const Box = new THREE.BoxGeometry(2, 2, 2)
    const meterial = new THREE.MeshStandardMaterial({color: 0xff0000})
    const mesh = new THREE.Mesh(Box, meterial)
    mesh.position.y+=1
    mesh.position.z+=4
    // scene.add(mesh)

    // const circle = new THREE.CircleGeometry(1,100);   //앞면만 렌더링되어있기 때문에 뒷면으로 카메라 이동하면 못봄
    // const mesh2 = new THREE.Mesh(circle, meterial)
    // mesh2.position.x+=4
    // mesh2.position.y+=1
    // scene.add(mesh2)

    const circle = new THREE.CylinderGeometry(1.5,1.5,0.5,10);
    const meterial2 = new THREE.MeshStandardMaterial({color: 0xff00ff})
    const mesh2 = new THREE.Mesh(circle, meterial2);
    mesh2.rotateX(- (Math.PI/2))
    mesh2.position.x+=4
    mesh2.position.y+=1
    // scene.add(mesh2)

    const sylinder = new THREE.CylinderGeometry(1, 1, 2, 3);   //위, 아래, 높이 ,쪼개는 정도
    const meterial3 = new THREE.MeshStandardMaterial({color: 0x0000ff})
    const mesh3 = new THREE.Mesh(sylinder, meterial3);
    mesh3.position.x-=4
    mesh3.position.y+=1
    // scene.add(mesh3)

    const sphere = new THREE.SphereGeometry(1, 4, 4)
    const meterial4 = new THREE.MeshStandardMaterial({color: 0x00ff00})
    const mesh4 = new THREE.Mesh(sphere, meterial4);
    mesh4.position.z-=4
    mesh4.position.y+=1
    mesh4.layers.enable(1);
    // scene.add(mesh4)

    const group = new THREE.Group()
    const group2 = new THREE.Group()
    group.add(mesh);
    group.add(mesh2);
    group.add(mesh3);
    group.add(mesh4);
    group2.add(mesh3.clone());
    group2.add(mesh4.clone());
    group.position.y+=2;
    
    scene.add(group);
    group.add(new THREE.AxesHelper(10))

    axisFolder.add(group.position, 'x', 0, 5, 0.2).name('x축')
    axisFolder.add(group.position, 'y', 0, 5, 0.2).name('y축')
    axisFolder.add(group.position, 'z', 0, 5, 0.2).name('z축')
    axisFolder.add(group2.position, 'y', 0, 5, 0.2).name('y축')
    scene.add(group2)

    ///////////////////////////
    //grid
    ///////////////////////////
  
    // const gridHelper = new THREE.GridHelper(30, 30)
    // const gridHelper2 = new THREE.GridHelper(30, 30)
    // const gridHelper3 = new THREE.GridHelper(30, 30)
    // const gridHelper4 = new THREE.GridHelper(30, 30)
    // gridHelper2.rotateX(-(Math.PI)/2)
    // gridHelper3.rotateZ(-(Math.PI)/2)
    // gridHelper4.rotateX(-(Math.PI)/2)
    // scene.add(gridHelper)
    // scene.add(gridHelper2)
    // scene.add(gridHelper3)
    // meshh.add(gridHelper4)

    // scene.add(new THREE.AxesHelper(10))
    // mesh4.add(new THREE.AxesHelper(3))

    /////////////////////////////
    //control
    ////////////////////////////

    const raycast = new THREE.Raycaster();
    // raycast.layers.set(1)
    const pointer = new THREE.Vector2();
    // raycast.setFromCamera(pointer, camera);
    // const intersects = raycast.intersectObject(scene.children);

    renderer.domElement.addEventListener('pointerdown', event =>{//pointerdown , pointermove, dbclick, contextmenu, dbclick
      const cx = event.clientX
      const cy = event.clientY
      const tx = event.offsetX  //offset 흰색공간
      const ty = event.offsetY  //offset 흰색 공간

      // console.log(cx)
      // console.log(cy)
      // console.log(tx)
      // console.log(ty)

      const boundX = cx - tx  //흰색공간 크기찾기
      const boundY = cy - ty

      // console.log(boundX)
      // console.log(boundY)
      
      const rx = cx-boundX    //그 크기 빼주기
      const ry = cy-boundY
      const width = renderer.domElement.clientWidth
      const height = renderer.domElement.clientHeight

      console.log(width)
      console.log(height)

      const x1 = rx/width
      const y1 = ry/height

      const wx = x1 * 2 - 1
      const wy = -y1 * 2 + 1

      pointer.set(wx, wy);

      console.log(pointer)

      raycast.setFromCamera(pointer, camera);
      const intersects = raycast.intersectObjects(scene.children)

      // const rancolor = THREE.MathUtils.randInt(0x000000,0xffffff);

      if(intersects){
        const intersect = intersects[0]
        // console.log(intersect)
        intersect.object.material.color.set(THREE.MathUtils.randInt(0x000000,0xffffff))
      }
      // console.log(renderer.domElement.Width)
  });

    window.addEventListener('resize', ()=>{
      camera.aspect=(window.innerWidth-20)/(window.innerHeight/2)
      camera.updateProjectionMatrix();
      renderer.setSize((window.innerWidth-20), (window.innerHeight/2))
    })

    render();
    function render(){
      renderer.render(scene, camera);       //렌더러는 맨 마지막에
      
      stats.update();

      // const time = de /1000
      // hemisphereLight.position.x += Math.cos(time)

      // PointLight.position.x+=0.01
      // PointLight.position.z+=0.01

      // rectareaLight.rotation.x += 0.01

      // mesh.rotation.x += 0.01
      // mesh.rotation.y += 0.01

      // mesh2.rotation.x += 0.01
      meshh.rotation.y+=0.01
      // meshh.scale.x+=0.0001
      // meshh.scale.z+=0.0001
      // meshh.scale.y+=0.0001

      mesh.rotation.y += 0.01
      mesh.rotation.x += 0.01

      mesh2.rotation.x += 0.01
      mesh2.rotation.z += 0.01

      mesh3.rotation.y += 0.01
      mesh3.rotation.z += 0.01

      mesh4.rotation.x += 0.01
      mesh4.rotation.y += 0.01
      // mesh2.rotation.y += 0.01
      // mesh2.rotation.z += 0.01

      requestAnimationFrame(render);
    }
  }
}
</script>

<style>

</style>
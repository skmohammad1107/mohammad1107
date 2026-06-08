npx create-react-app 3d-data-analyst-portfolio
cd 3d-data-analyst-portfolio

npm install three @react-three/fiber @react-three/drei
import React from "react";
import { Canvas } from "@react-three/fiber";
import { OrbitControls, Float } from "@react-three/drei";
import DataCube from "./components/DataCube";
import SkillsSphere from "./components/SkillsSphere";

export default function Scene() {
  return (
    <Canvas camera={{ position: [0, 2, 6] }}>
      <ambientLight intensity={0.5} />
      <directionalLight position={[5, 5, 5]} intensity={1} />

      <Float speed={2} rotationIntensity={1}>
        <DataCube position={[-2, 0, 0]} />
      </Float>

      <Float speed={2}>
        <SkillsSphere position={[2, 0, 0]} />
      </Float>

      <OrbitControls enableZoom={true} />
    </Canvas>
  );
}

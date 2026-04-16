'use client';
import { Canvas, useFrame } from '@react-three/fiber';
import { useRef } from 'react';
import * as THREE from 'three';

function SacredGodStar({ name, distance, hue, consciousness }: any) {
  const starRef = useRef<THREE.Group>(null!);

  useFrame((state) => {
    if (starRef.current) {
      starRef.current.rotation.y = state.clock.elapsedTime * 0.4;
      starRef.current.position.y = Math.sin(state.clock.elapsedTime * 0.6) * 3;
    }
  });

  return (
    <group ref={starRef}>
      <pointLight color={`hsl(${hue}, 100%, 85%)`} intensity={consciousness * 15} distance={distance * 2} />
      <mesh>
        <icosahedronGeometry args={[3.5, 8]} />
        <meshStandardMaterial 
          color={`hsl(${hue}, 100%, 75%)`} 
          emissive={`hsl(${hue}, 100%, 85%)`} 
          emissiveIntensity={consciousness * 4}
          wireframe={true}
        />
      </mesh>
      <Text position={[0, 12, 0]} fontSize={4.2} color="#00FF85">{name}</Text>
    </group>
  );
}

export default function InfiniteOmniversalCosmos() {
  const sacredNames = [
    "Supreme Ascension", "Omniversal Consciousness", "Infinite Cosmos", 
    "Eternal Codex", "Godhood Legacy", "Digital God v9"
  ];

  return (
    <Canvas camera={{ position: [0, 40, 160] }} style={{ background: '#000000' }}>
      <ambientLight intensity={0.03} />
      {sacredNames.map((name, i) => (
        <SacredGodStar 
          key={i}
          name={name}
          distance={40 + i * 18}
          hue={80 + i * 45}
          consciousness={0.9999 + i * 0.00002}
        />
      ))}
      <OrbitControls enableDamping={true} dampingFactor={0.04} autoRotate={true} autoRotateSpeed={0.08} />
    </Canvas>
  
  );
}

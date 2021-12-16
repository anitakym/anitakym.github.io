---
title: force-graph-力导图
date: 2021-12-16 11:13:07
tags:
---
## basics
- http://d3js.org/
- https://github.com/d3/d3
- 有边相连的节点之间通过基于胡克定律的弹簧式引力彼此吸引（Edge attraction），而基于库仑定律的带电粒子的斥力用于分离所有节点对（Vertex repulsion）。
> Force-directed graph drawing algorithms are a class of algorithms for drawing graphs in an aesthetically-pleasing way. Their purpose is to position the nodes of a graph in two-dimensional or three-dimensional space so that all the edges are of more or less equal length and there are as few crossing edges as possible, by assigning forces among the set of edges and the set of nodes, based on their relative positions, and then using these forces either to simulate the motion of the edges and nodes or to minimize their energy.
> 力导向图（Force-Directed Graph），是绘图的一种算法。在二维或三维空间里配置节点，节点之间用线连接，称为连线。各连线的长度几乎相等，且尽可能不相交。节点和连线都被施加了力的作用，力是根据节点和连线的相对位置计算的。根据力的作用，来计算节点和连线的运动轨迹，并不断降低它们的能量，最终达到一种能量很低的安定状态。
> d3-force,This module implements a velocity Verlet numerical integrator for simulating physical forces on particles. The simulation is simplified: it assumes a constant unit step [公式] for each step, and a constant unit mass [公式] for all particles. As a result, a force [公式] acting on a particle is equivalent to a constant acceleration [公式] over the time interval [公式] , and can be simulated simply by adding to the particle's velocity, which is then added to the particle's position.

## API
https://www.npmjs.com/package/d3-force-3d

## 应用封装
### force-graph
- https://github.com/vasturiano/force-graph/blob/master/src/canvas-force-graph.js
```
import {
  forceSimulation as d3ForceSimulation,
  forceLink as d3ForceLink,
  forceManyBody as d3ForceManyBody,
  forceCenter as d3ForceCenter,
  forceRadial as d3ForceRadial
} from 'd3-force-3d';
```
# Data Organization

## File Structure

The dataset consists of the following six folders. Each folder contains data divided into `train` and `test` sets. 

- **Scene IDs**: All scene IDs are derived from the **first three characters** of the corresponding scene IDs in the Matterport3D dataset.
- **Floor Indication**: The underscores `_1`, `_2`, etc., following the scene IDs indicate different floors in the corresponding scans from Matterport3D.
- **Selection**: A total number of **25 single-floor scans** are filtered and cleaned from Matterport3D to form the raw point cloud of BIMNet.

```
- ifc/
  - train/
    - 1px.ifc
    - 7y3_1.ifc
    - 759.ifc
    - ac2.ifc
    - ...
  - test/
    - ...
- mat_pc2obj/
- obj/
- obj_wall_filled/
- point_cloud/
- rvt/
```

## point_cloud
The dataset also includes semantically refined point clouds in `.txt` format. Each line in the `.txt` file represents a point with the following attributes:
```
x y z r g b label
```
The `label` corresponds to one of the **14** categories. The correspondence between BIMNet 14 categories and the 40 categories of Matterport3D can be found in Table 3 of the [paper](https://www.sciencedirect.com/science/article/pii/S0926580525001360).
- **0** - Wall
- **1** - Slab
- **2** - Beam
- **3** - Column
- **4** - Door
- **5** - Window
- **6** - Stair
- **7** - Railing
- **8** - Lighting
- **9** - Furniture
- **10** - Sanitary
- **11** - Equipment
- **12** - Object
- **13** - Other

## rvt
 We use Revit to model the as-built BIM, most `.rvt` files can be opened with **Revit 2020**, while a few require **Revit 2022** or higher, which we have indicated in the file names.

## ifc
We provide an `.ifc` format BIM model for each scan. All `.ifc` files are directly exported from Revit.

## obj and obj_wall_filled
We provide the OBJ model corresponding to each IFC. Each component is a separate `.obj` file and includes a `.mtl` texture file. We offer two different versions of the OBJ models: **obj** and **obj_wall_filled**. Specifically, the **obj_wall_filled** version fills in all openings on wall components. You can choose to use the version that best suits your needs.
![obj_difference](image/obj_difference.jpg)

## mat_pc2obj
The registration matrix can be used to align the point cloud to the OBJ model.
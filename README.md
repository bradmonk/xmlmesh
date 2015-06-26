# xmlmesh()

xmlmesh is a Matlab function to format triangulated mesh data for xml file output.


## Syntax
-----------------------------------------------------
    xmlmesh(vrts,tets)
    xmlmesh(vrts,tets,'filename.xml')
    xmlmesh(____,'doctype','xmlns')


## Description
-----------------------------------------------------
    xmlmesh() takes a set of 2D or 3D vertices (vrts) and a tetrahedral (tets)
    connectivity list, and creates an XML file of the mesh. This function was
    originally created to export xml mesh files for using in Fenics:Dolfin
    but can be adapted for universal xml export of triangulated meshes.


## Useage Definitions
-----------------------------------------------------


    xmlmesh(vrts,tets)
        creates an XML file 'xmlmesh.xml' from a set of vertices "vrts"
        and a connectivity list; here the connectivity list is referred
        to as "tets". These parameters can be generated manually, or by
        using matlab's builtin triangulation functions. The point list
        "vrts" is a matrix with dimensions Mx2 (for 2D) or Mx3 (for 3D).
        The matrix "tets" represents the triangulated connectivity list
        of size Mx3 (for 2D) or Mx4 (for 3D), where M is the number of
        triangles. Each row of tets specifies a triangle defined by indices
        with respect to the points. The delaunayTriangulation function
        can be used to quickly generate these input variables:
            TR = delaunayTriangulation(XYZ);
            vrts = TR.Points;
            tets = TR.ConnectivityList;


    xmlmesh(vrts,tets,'filename.xml')
        same as above, but allows you to specify the xml filename.


    xmlmesh(____,'doctype','xmlns')
        same as above, but allows you to additionally specify the
        xml namespace xmlns attribute. For details see:
        http://www.w3schools.com/xml/xml_namespaces.asp




## Example
-----------------------------------------------------

% Create 2D triangulated mesh
    XY = randn(10,2);
    TR2D = delaunayTriangulation(XY);
    vrts = TR2D.Points;
    tets = TR2D.ConnectivityList;

    xmlmesh(vrts,tets,'xmlmesh_2D.xml')


% Create 3D triangulated mesh
    d = [-5 8];
    [x,y,z] = meshgrid(d,d,d); % a cube
    XYZ = [x(:) y(:) z(:)];
    TR3D = delaunayTriangulation(XYZ);
    vrts = TR3D.Points;
    tets = TR3D.ConnectivityList;

    xmlmesh(vrts,tets,'xmlmesh_3D.xml')


## Example Output
--------------------------


% From 2D xml mesh file: xmlmesh_2D.xml

    <?xml version="1.0" encoding="utf-8"?>
    <dolfin xmlns:dolfin="bradleymonk.com/xmlmesh">
       <mesh celltype="tetrahedron" dim="2">
          <vertices size="10">
             <vertex index="0" x="-2.9375e-01" y="-1.33200e+00"/>
             <vertex index="1" x="-8.4792e-01" y="-2.32986e+00"/>
             <vertex index="2" x="-1.1201e+00" y="-1.44909e+00"/>
             <vertex index="3" x="2.52599e+00" y="3.335108e-01"/>
             <vertex index="4" x="1.65549e+00" y="3.913536e-01"/>
             <vertex index="5" x="3.075351e-01" y="4.51679e-01"/>
             <vertex index="6" x="-1.25711e+00" y="-1.3028e-01"/>
             <vertex index="7" x="-8.65468e-01" y="1.83689e-01"/>
             <vertex index="8" x="-1.76534e-01" y="-4.7615e-01"/>
             <vertex index="9" x="7.914160e-01" y="8.62021e-01"/>
          </vertices>
          <cells size="12">
             <tetrahedron index="0" v0="2" v1="1" v2="0"/>
             <tetrahedron index="1" v0="5" v1="9" v2="7"/>
             <tetrahedron index="2" v0="2" v1="0" v2="8"/>
             <tetrahedron index="3" v0="6" v1="2" v2="8"/>
             <tetrahedron index="4" v0="8" v1="5" v2="7"/>
             <tetrahedron index="5" v0="8" v1="4" v2="5"/>
             <tetrahedron index="6" v0="4" v1="3" v2="9"/>
             <tetrahedron index="7" v0="6" v1="8" v2="7"/>
             <tetrahedron index="8" v0="0" v1="4" v2="8"/>
             <tetrahedron index="9" v0="5" v1="4" v2="9"/>
             <tetrahedron index="10" v0="0" v1="1" v2="3"/>
             <tetrahedron index="11" v0="0" v1="3" v2="4"/>
          </cells>
       </mesh>
    </dolfin>



% From 3D xml mesh file: xmlmesh_3D.xml

    <?xml version="1.0" encoding="utf-8"?>
    <dolfin xmlns:dolfin="bradleymonk.com/xmlmesh">
       <mesh celltype="tetrahedron" dim="3">
          <vertices size="8">
             <vertex index="0" x="-5.00000e+00" y="-5.0000e+00" z="-5.00000e+00"/>
             <vertex index="1" x="-5.00000e+00" y="8.00000e+00" z="-5.00000e+00"/>
             <vertex index="2" x="8.00000e+00" y="-5.00000e+00" z="-5.00000e+00"/>
             <vertex index="3" x="8.00000e+00" y="8.00000e+00" z="-5.00000e+00"/>
             <vertex index="4" x="-5.00000e+00" y="-5.0000e+00" z="8.00000e+00"/>
             <vertex index="5" x="-5.00000e+00" y="8.00000e+00" z="8.00000e+00"/>
             <vertex index="6" x="8.00000e+00" y="-5.00000e+00" z="8.00000e+00"/>
             <vertex index="7" x="8.00000e+00" y="8.00000e+00" z="8.00000e+00"/>
          </vertices>
          <cells size="6">
             <tetrahedron index="0" v0="4" v1="0" v2="1" v3="2"/>
             <tetrahedron index="1" v0="5" v1="4" v2="1" v3="2"/>
             <tetrahedron index="2" v0="5" v1="6" v2="4" v3="2"/>
             <tetrahedron index="3" v0="5" v1="3" v2="6" v3="2"/>
             <tetrahedron index="4" v0="5" v1="1" v2="3" v3="2"/>
             <tetrahedron index="5" v0="5" v1="7" v2="6" v3="3"/>
          </cells>
       </mesh>
    </dolfin>




## See Also
-----------------------------------------------------
http://bradleymonk.com/xmlmesh
http://fenicsproject.org
>> web(fullfile(docroot, 'matlab/math/triangulation-representations.html'))


## Attribution
-----------------------------------------------------
% Created by: Bradley Monk
% email: brad.monk@gmail.com
% website: bradleymonk.com
% 2015.06.25


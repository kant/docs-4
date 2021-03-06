Digitizing Channels 
===============================

General
-------

QGEP has a wizard to correctly build channels and connect them to wastewater structures respectively to wastewater nodes or other reaches (building up the topology for waste water nodes and reaches).

.. attention:: There is an error with the wizard in qgep plugin version 1.1.4. See QGEP Issue #443 and #451.

.. figure:: images/wizard_data_entry.jpg

.. figure:: images/wizard_data_entry_reach.jpg

.. attention:: Start digitizing in the direction of the flow by starting with the
  **from manhole node** and finishing with the **to manhole node**. 

.. Note:: There is now a tool to change the flow direction (topology), but there is still a problem with storing the changed channels. See QGEP Issue #380.

Digitizing
----------

* In digitizing mode the cursor will automatically snap to the nearest cover or reach.
  When left clicking a line starts to draw.

.. figure:: images/wizard_data_entry_reach_with_new_cursor3.jpg

* With further left clicks anywhere you can define intermediary points of the reach progression.
  You can also directly select another manhole to draw a straight channel.

.. figure:: images/wizard_data_entry_reach_with_new_cursor2-3.jpg

* You finish digitizing the line by right clicking. This will make the **vw_qep_reach** form appear.

.. figure:: images/wizard_wastewater_structure_reach_form3.jpg

.. note:: Keep in mind that the finishing point of the line is the last point where you **left** clicked.
  Thus, for digitizing a simple line with 2 points you need two **left clicks** to digitize the line and one
  **right click** to finish the line digitizing. 

* Add the attributes on the **General** tab. 

.. note:: Control the snapping to wastewater nodes or other reaches in the fields **rp_from/to_fk_wastewater_networkelement**

* For the profile type you will get a list of defined profiles.
  You can edit those in **od_pipe_profile** table.

.. figure:: images/wizard_wastewater_structure_reach_form_profiles3.jpg


* When finished, then click the **OK** button. 

* Save the information of this layer by stopping the data entry wizard.

.. figure:: images/stop_data_entry.jpg

* You can re-edit your object selecting the edit mode and then click with the info cursor on the object you want to edit.
* If you do not select the edit mode, you can just look add the existing data.

.. figure:: images/reach_info_reach3.jpg

* For detailed information about editing see the :ref:`editing-data` chapter.


Further attributes and classes
------------------------------

When a line object is digitized a series of steps take place in the background in the QGEP database:

* an new object is added in the **wastewater structure** class (``od_wastewater_structure``)
* a new object is added and linked in the **channel** subclass (``od_channel``)
* two new reach point objects are added and linked to the reach (**rp_from_node**, **rp_to_node**)

.. figure:: images/reach_form_reach_points3.jpg

* a new reach object is generated in the **wastewater network elements** class (``od_wastewater_networkelement``)
  and its subclass **reach** (``od_reach``)


Geometry synchronization
------------------------

The start- and the end-point of the added feature's geometry defines the reach point's geometries. The altitude (Z value of geometry) of the added feature's start- and the end-point is defined by the level values `rp_from_level` and `rp_to_level`. This means, the Z values of the reach point's geometry is set by the level as well. These values could be filled up by the snapped features:

.. figure::images/reach_geometry_snapping_01.jpg

The snapped features 9405 and 9390 have the altitude from the cover levels: 424.090 and 422.900. These values are entered into the attributes `rp_from_level` and `rp_to_level` and can be edited there by the user. When the user changes these values, the Z value of the geometry of the digitized feature and its reach points will be changed as well. 

.. figure::images/reach_geometry_snapping_02.jpg

.. note:: If a reach point's level changes, the Z value of its geometry changes, and so does the start- or the end-point of the reach. When the Z value of the reach's geometry changes, the reach point's geometry and its level is ajusted as well. If both values change, the level takes precendence. On an insert it's like when both value change. Means the reach's geometry is set according to the reach point's levels and if they are NULL, the Z value of the reach's start- and end-point are set to NaN.

TO DO Documentation
---------------------

* take more from GEPView-Howto 1.2. Chapter 4.2)
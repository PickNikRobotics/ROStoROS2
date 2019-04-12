ROS to ROS2 Porting Guide
=========================

Fully Automatable Transforms
----------------------------
- Changing msg, srv, and action includes in C++ files
    - ROS:    ``#include <std_msgs/ColorRGBA.h>``
    - ROS2:   ``#include <std_msgs/msg/color_rgba.hpp>``
    - Example Script: todo

- Changing msg, srv, and action namespacing in C++ files
    - ROS:    ``geometry_msgs::Pose``
    - ROS2:   ``geometry_msgs::msg::Pose``
    - Example Script: todo

- Changing the logging
    - A first pass of this can be done automatically, but it is better to use the node's logger when possible
    - Example Script: todo

- ``package.xml`` changes
    - Changing from format 1->3 and 2->3
        - ROS:
            - ``<package>``
            - ``<package format="1">``
            - ``<package format="2">``
        - ROS2:
            - ``<package format="3">``
        - *Note*: Technically, you can still use version 2 unless you are generating custom msgs
        - Example Script: todo
    - Changing ``buildtool_depend`` to ``ament_cmake``
        - ROS:    ``<buildtool_depend>catkin</buildtool_depend>``
        - ROS2:   ``<buildtool_depend>ament_cmake</buildtool_depend>``
        - Example Script: todo
    - Adding ``<member_of_group>rosidl_interface_packages</member_of_group>`` to any package that creates custom msgs, srvs or actions
        - Example Script: todo
    - Changing ``run_depend`` to ``exec_depend``
        - Example Script: todo
    - Adding ``<build_type>ament_cmake</build_type>`` inside ``<export> ... </export>`` tags
        - Example Script: todo
    - Changing ``message_runtime`` to ``rosidl_default_runtime``
        - Example Script: todo
    - Changing ``message_generation`` to ``rosidl_default_generators``
        - Example Script: todo

- ``CMakeLists.txt`` changes
    - Change msg file generation:
        - Transform 1:
            - ROS:  ``add_message_files( .... FILES``
            - ROS2: ``rosidl_generate_interfacesrosidl_generate_interfaces(${PROJECT_NAME}``
        - Transform 2:
            - ROS:  ``<msg_name>.msg``
            - ROS2: ``"msg/<msg_name>.msg"``
    - Change srv file generation:
        - Transform 1:
            - ROS:  ``add_service_files( .... FILES``
            - ROS2: ``rosidl_generate_interface(${PROJECT_NAME}``
        - Transform 2:
            - ROS:  ``<srv_name>.srv``
            - ROS2: ``"srv/<srv_name>.srv"``
    - Change action file generation:
        - Transform 1:
            - ROS:  ``add_action_files( .... FILES``
            - ROS2: ``rosidl_generate_interface(${PROJECT_NAME}``
        - Transform 2:
            - ROS:  ``<action_name>.action``
            - ROS2: ``"action/<srv_name>.action"``
            - *NOTE:* You will have to manually move ``DEPENDENCIES`` from ``generate_messages(`` to within the ``rosidl_generate_interface`` command

More Involved Transforms
------------------------
- Create ros1_bridge mapping rules
- Transforming publishers, subscribers, servers and clients
- Tranforming node handles to nodes
- Changing plugin registering and loading. (See `RViz2 plugin development doc <https://github.com/ros2/rviz/blob/ros2/docs/plugin_development.md>`_)
- Transforming nodelets to nodes with composition
- Executors and Node strategy
- Catkin to Ament (CMakeListst.txt)



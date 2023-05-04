FROM osrf/ros:melodic-desktop-full

# Instalar dependencia que falta para el paquete
RUN apt-get update && \
   apt-get install -y ros-melodic-joint-state-publisher-gui && \
   apt-get install ros-melodic-joint-trajectory-controller && \
   apt-get install ros-melodic-rqt-joint-trajectory-controller && \
   rm -rf /var/lib/apt/lists/*

# Crear espacio de trabajo catkin_ws/src
RUN mkdir -p /root/catkin_ws/src/robot_scara

# Copiar el paquete a la carpeta src del workspace
COPY robot_scara /root/catkin_ws/src/robot_scara

# Compilar el paquete en el workspace
RUN /bin/bash -c "source /opt/ros/melodic/setup.bash && \
                  cd /root/catkin_ws && \
                  catkin_make && \
                  source devel/setup.bash"

RUN /bin/bash -c 'echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc'

# Establecer el workspace como directorio de trabajo predeterminado
WORKDIR /root/catkin_ws
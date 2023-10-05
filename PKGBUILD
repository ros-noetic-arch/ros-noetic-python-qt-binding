pkgdesc="ROS - This stack provides Python bindings for Qt."
url='https://wiki.ros.org/python_qt_binding'

pkgname='ros-noetic-python-qt-binding'
pkgver='0.4.4'
arch=('any')
pkgrel=3
license=('BSD')

ros_makedepends=(
    ros-noetic-catkin
    ros-noetic-rosbuild
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
    qt5-base
)

ros_depends=(
)

depends=(
    ${ros_depends[@]}
    python-pyqt5-sip
)

_dir="python_qt_binding-${pkgver}"
source=(
    "${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-visualization/python_qt_binding/archive/${pkgver}.tar.gz"
    "sip.patch"
)
sha256sums=(
    'bcb5076226100f901e6a22656cf69ef0e8d5f1845670e6fad6fc5fdcb3a1dd07'
    'e46282ccc7851c39916164d9919af4b8774f46137b5986148e75d45e4547ef46'
)

prepare() {
    cd ${srcdir}/${_dir}
    patch -p1 -i "${srcdir}/sip.patch"
}

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}

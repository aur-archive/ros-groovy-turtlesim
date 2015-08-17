pkgdesc="ROS - turtlesim"
url='http://www.ros.org/'

pkgname='ros-groovy-turtlesim'
pkgver='0.3.12'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-catkin
  ros-groovy-message-generation
  ros-groovy-roscpp
  ros-groovy-roscpp-serialization
  ros-groovy-rosconsole
  ros-groovy-roslib
  ros-groovy-rostime
  ros-groovy-std-msgs
  ros-groovy-std-srvs
  qt4
)

source=(qtboost.patch)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/turtlesim ]; then
    cd ${srcdir}/turtlesim
    git fetch origin --tags
    git reset --hard release/groovy/turtlesim/${pkgver}-0
  else
    git clone -b release/groovy/turtlesim/${pkgver}-0 git://github.com/ros-gbp/ros_tutorials-release.git ${srcdir}/turtlesim
  fi
  cd ${srcdir}
  patch -Np1 -i qtboost.patch
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/turtlesim
  cmake ${srcdir}/turtlesim -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
md5sums=('cdff718bdb5954eed58eed27cfdae70b')

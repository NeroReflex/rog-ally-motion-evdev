pkgname=rog-ally-motion-evdev
pkgver=1.0.0
pkgrel=1
pkgdesc='Exposes bmi323 chip over an evdev interface'
arch=('x86_64')
url='https://github.com/NeroReflex/ally-motion-evdev/'
license=('BSD')
depends=()
makedepends=('cmake')
provides=('ally-motion-evdev')
source=(
    "ally-motion-evdev::git+https://github.com/NeroReflex/ally-motion-evdev.git"
    "ally-motion-evdev.service"
    "10-ally-motion-evdev.rule"
)
sha256sums=(
    'SKIP'
    'b4eaf36b99d0565d31d77d1a3872fb5eae94075dc078b8ccf137634a39232dd6' # ally-motion-evdev.service
    '6954a9e1c614be8ff7ebf5456713d31735f1d3b0dfc92365e2c378ca3e99de6d' # 10-ally-motion-evdev.rule
)

prepare() {
    cd "ally-motion-evdev"
    #mkdir "ally-motion-evdev/build"
    cd ..
}

build() {
    cmake \
        -B build \
        -S "ally-motion-evdev" \
        -G 'Unix Makefiles' \
        -DCMAKE_BUILD_TYPE:STRING='Release' \
        -DCMAKE_INSTALL_PREFIX:PATH='/usr' \
        -Wno-dev
    cmake --build build
}

#check() {
#    ctest --test-dir build --output-on-failure
#}

package() {
    DESTDIR="$pkgdir" cmake --install build
    #cd "${pkgname}-${pkgver}"
    
    # udev
    install -D -m644 10-ally-motion-evdev.rule   -t "${pkgdir}/usr/lib/udev/rules.d/"

    # systemd
    install -D -m644 ally-motion-evdev.service   -t "${pkgdir}/usr/lib/systemd/user/"
    
    # license
    #install -D -m644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

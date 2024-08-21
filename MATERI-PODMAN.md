# PERCEPATAN STUDI MATA KULIAH TEKNOLOGI CLOUD
```
nama maswandi
nim 185610057
````
![PODMAN logo](https://raw.githubusercontent.com/containers/common/main/logos/podman-logo-full-vert.png)

# Podman: Alat untuk mengelola kontainer dan pod OCI

Podman (POD MANager) adalah alat untuk mengelola kontainer dan gambar, volume yang dipasang ke dalam kontainer tersebut, dan pod yang dibuat dari kelompok kontainer.
Podman menjalankan kontainer di Linux, tetapi juga dapat digunakan pada sistem Mac dan Windows menggunakan mesin virtual yang dikelola Podman.
Podman didasarkan pada libpod, pustaka untuk manajemen siklus hidup kontainer yang juga terdapat dalam repositori ini. Pustaka libpod menyediakan API untuk mengelola kontainer, pod, gambar kontainer, dan volume.


Semua rilis ditandatangani PGP. Kunci publik anggota tim yang disetujui untuk membuat rilis berada di [sini](https://github.com/containers/release-keys/tree/main/podman).

* download disini:
  * [Downloads](DOWNLOADS.md)

## Gambaran umum dan cakupan

Pada tingkat tinggi, cakupan Podman dan libpod adalah sebagai berikut:

* Dukungan untuk beberapa format citra kontainer, termasuk citra OCI dan Docker.
* Manajemen penuh atas citra tersebut, termasuk penarikan dari berbagai sumber (termasuk kepercayaan dan verifikasi), pembuatan (dibuat melalui Containerfile atau Dockerfile atau dikomit dari kontainer), dan pengiriman ke registri dan backend penyimpanan lainnya.
* Manajemen penuh atas siklus hidup kontainer, termasuk pembuatan (baik dari citra maupun dari sistem berkas root yang dieksplorasi), menjalankan, melakukan checkpointing, dan memulihkan (melalui CRIU), dan penghapusan.
* Manajemen penuh atas jaringan kontainer, menggunakan Netavark.
* Dukungan untuk pod, kelompok kontainer yang berbagi sumber daya dan dikelola bersama.
* Dukungan untuk menjalankan kontainer dan pod tanpa hak akses root atau hak istimewa tinggi lainnya.
* Isolasi sumber daya kontainer dan pod.
* Dukungan untuk antarmuka CLI yang kompatibel dengan Docker, yang dapat menjalankan kontainer secara lokal dan pada sistem jarak jauh.
* Tidak ada daemon manajer, untuk meningkatkan keamanan dan mengurangi penggunaan sumber daya saat tidak aktif.
* Dukungan untuk REST API yang menyediakan antarmuka yang kompatibel dengan Docker dan antarmuka yang ditingkatkan yang memperlihatkan fungsionalitas Podman tingkat lanjut.

* Dukungan untuk berjalan di Windows dan Mac melalui mesin virtual yang dijalankan oleh `podman machine`.

## Peta jalan

1. Peningkatan lebih lanjut pada `podman machine` untuk mendukung Podman Desktop dan kasus penggunaan pengembang lainnya dengan lebih baik.
1. Dukungan untuk [conmon-rs](https://github.com/containers/conmon-rs), yang akan meningkatkan pencatatan kontainer.
1. Dukungan untuk BuildKit API.
1. Peningkatan kinerja dan stabilitas.
1. Pengurangan ukuran biner Podman.

## Komunikasi

Jika Anda merasa telah mengidentifikasi masalah keamanan dalam proyek, mohon *JANGAN* melaporkan masalah tersebut secara publik melalui pelacak masalah GitHub, milis, atau IRC.

Sebaliknya, kirimkan email dengan detail sebanyak mungkin ke `security@lists.podman.io`. Ini adalah milis pribadi untuk pengelola inti.

Untuk pertanyaan dan diskusi umum, mohon gunakan
[saluran](https://podman.io/community/#slack-irc-matrix-and-discord) Podman.

Untuk diskusi seputar masalah/bug dan fitur, Anda dapat menggunakan sistem pelacakan
[masalah](https://github.com/containers/podman/issues)
dan
[PR](https://github.com/containers/podman/pulls)
GitHub.

Ada juga [milis](https://lists.podman.io/archives/) di `lists.podman.io`.
Anda dapat berlangganan dengan mengirimkan pesan ke `podman-join@lists.podman.io` dengan subjek `subscribe`.

## Tanpa Root
Podman dapat dengan mudah dijalankan sebagai pengguna normal, tanpa memerlukan biner setuid.
Saat dijalankan tanpa root, kontainer Podman menggunakan namespace pengguna untuk menetapkan root dalam kontainer kepada pengguna yang menjalankan Podman.
Podman tanpa root menjalankan kontainer yang terkunci tanpa hak istimewa yang tidak dimiliki pengguna yang menjalankan kontainer.
Beberapa pembatasan ini dapat dicabut (melalui `--privileged`, misalnya), tetapi kontainer tanpa root tidak akan pernah memiliki hak istimewa lebih dari pengguna yang meluncurkannya.
Jika Anda menjalankan Podman sebagai pengguna dan memasang di `/etc/passwd` dari host, Anda tetap tidak akan dapat mengubahnya, karena pengguna Anda tidak memiliki izin untuk melakukannya.

Hampir semua fungsionalitas Podman normal tersedia, meskipun ada beberapa [kekurangan](https://github.com/containers/podman/blob/main/rootless.md). Setiap rilis Podman terbaru seharusnya dapat berjalan tanpa root tanpa konfigurasi tambahan, meskipun sistem operasi Anda mungkin memerlukan beberapa konfigurasi tambahan yang dijelaskan secara terperinci dalam [panduan instalasi](https://podman.io/getting-started/installation).

Sedikit konfigurasi oleh administrator diperlukan sebelum Podman tanpa root dapat digunakan, pengaturan yang diperlukan didokumentasikan [di sini](https://github.com/containers/podman/blob/main/docs/tutorials/rootless_tutorial.md).

## Podman Desktop

[Podman Desktop](https://podman-desktop.io/) menyediakan lingkungan pengembangan lokal untuk Podman dan Kubernetes pada mesin Linux, Windows, dan Mac.
Ini adalah frontend UI desktop berfitur lengkap untuk Podman yang menggunakan backend `podman machine` pada sistem operasi non-Linux untuk menjalankan kontainer.
Mendukung manajemen siklus hidup kontainer secara penuh (membuat, menarik, dan mendorong gambar, membuat dan mengelola kontainer, membuat dan mengelola pod, dan bekerja dengan Kubernetes YAML).
Proyek ini dikembangkan di [GitHub](https://github.com/containers/podman-desktop) dan kontribusi diterima dengan senang hati.

## Di luar cakupan

* Penandatanganan dan pengiriman gambar secara khusus ke berbagai backend penyimpanan.
Lihat [Skopeo](https://github.com/containers/skopeo/) untuk tugas tersebut.
* Dukungan untuk antarmuka Kubernetes CRI untuk manajemen kontainer.
Daemon [CRI-O](https://github.com/cri-o/cri-o) mengkhususkan diri dalam hal itu.

## Rencana Proyek OCI

Podman menggunakan proyek OCI dan pustaka terbaik untuk berbagai aspek:
- Runtime: Kami menggunakan [alat runtime OCI](https://github.com/opencontainers/runtime-tools) untuk menghasilkan konfigurasi runtime OCI yang dapat digunakan dengan runtime yang sesuai dengan OCI, seperti [crun](https://github.com/containers/crun/) dan [runc](https://github.com/opencontainers/runc/).
- Gambar: Manajemen gambar menggunakan pustaka [containers/image](https://github.com/containers/image).
- Penyimpanan: Penyimpanan kontainer dan gambar dikelola oleh [containers/storage](https://github.com/containers/storage).
- Jaringan: Dukungan jaringan melalui penggunaan [Netavark](https://github.com/containers/netavark) dan [Aardvark](https://github.com/containers/aardvark-dns). Jaringan tanpa root ditangani melalui [slirp4netns](https://github.com/rootless-containers/slirp4netns).
- Build: Build didukung melalui [Buildah](https://github.com/containers/buildah).
- Conmon: [Conmon](https://github.com/containers/conmon) adalah alat untuk memantau runtime OCI, yang digunakan oleh Podman dan CRI-O.
- Seccomp: Kebijakan [Seccomp](https://github.com/containers/common/blob/main/pkg/seccomp/seccomp.json) terpadu untuk Podman, Buildah, dan CRI-O.

## Podman Information for Developers

For blogs, release announcements and more, please checkout the [podman.io](https://podman.io) website!

**[Installation notes](install.md)**
Information on how to install Podman in your environment.

**[OCI Hooks Support](https://github.com/containers/common/blob/main/pkg/hooks/README.md)**
Information on how Podman configures [OCI Hooks][spec-hooks] to run when launching a container.

**[Podman API](https://docs.podman.io/en/latest/_static/api.html)**
Documentation on the Podman REST API.

**[Podman Commands](https://podman.readthedocs.io/en/latest/Commands.html)**
A list of the Podman commands with links to their man pages and in many cases videos
showing the commands in use.

**[Podman Container Images](https://github.com/containers/image_build/blob/main/podman/README.md)**
Information on the Podman Container Images found on [quay.io](https://quay.io/podman/stable).

**[Podman Troubleshooting Guide](troubleshooting.md)**
A list of common issues and solutions for Podman.

**[Podman Usage Transfer](transfer.md)**
Useful information for ops and dev transfer as it relates to infrastructure that utilizes Podman.  This page
includes tables showing Docker commands and their Podman equivalent commands.

**[Tutorials](docs/tutorials)**
Tutorials on using Podman.

**[Remote Client](https://github.com/containers/podman/blob/main/docs/tutorials/remote_client.md)**
A brief how-to on using the Podman remote client.

**[Basic Setup and Use of Podman in a Rootless environment](https://github.com/containers/podman/blob/main/docs/tutorials/rootless_tutorial.md)**
A tutorial showing the setup and configuration necessary to run Rootless Podman.

**[Release Notes](RELEASE_NOTES.md)**
Release notes for recent Podman versions.

**[Contributing](CONTRIBUTING.md)**
Information about contributing to this project.

[spec-hooks]: https://github.com/opencontainers/runtime-spec/blob/v1.0.2/config.md#posix-platform-hooks

## Buildah and Podman relationship

Buildah and Podman are two complementary open-source projects that are
available on most Linux platforms and both projects reside at
[GitHub.com](https://github.com) with Buildah
[here](https://github.com/containers/buildah) and Podman
[here](https://github.com/containers/podman).  Both, Buildah and Podman are
command line tools that work on Open Container Initiative (OCI) images and
containers.  The two projects differentiate in their specialization.

Buildah specializes in building OCI images.  Buildah's commands replicate all
of the commands that are found in a Dockerfile.  This allows building images
with and without Dockerfiles while not requiring any root privileges.
Buildah’s ultimate goal is to provide a lower-level coreutils interface to
build images.  The flexibility of building images without Dockerfiles allows
for the integration of other scripting languages into the build process.
Buildah follows a simple fork-exec model and does not run as a daemon
but it is based on a comprehensive API in golang, which can be vendored
into other tools.

Podman specializes in all of the commands and functions that help you to maintain and modify
OCI images, such as pulling and tagging.  It also allows you to create, run, and maintain those containers
created from those images.  For building container images via Dockerfiles, Podman uses Buildah's
golang API and can be installed independently from Buildah.

A major difference between Podman and Buildah is their concept of a container.  Podman
allows users to create "traditional containers" where the intent of these containers is
to be long lived.  While Buildah containers are really just created to allow content
to be added back to the container image.  An easy way to think of it is the
`buildah run` command emulates the RUN command in a Dockerfile while the `podman run`
command emulates the `docker run` command in functionality.  Because of this and their underlying
storage differences, you can not see Podman containers from within Buildah or vice versa.

In short, Buildah is an efficient way to create OCI images while Podman allows
you to manage and maintain those images and containers in a production environment using
familiar container cli commands.  For more details, see the
[Container Tools Guide](https://github.com/containers/buildah/tree/main/docs/containertools).

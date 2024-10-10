
cmake_minimum_required(VERSION 3.18.1)


project("prootapk")
set(CMAKE_ANDROID_ARCH_ABI "arm64-v8a")
enable_language(C ASM) #设置支持的语言，C 和 ASM（内联汇编）

add_compile_options(-DHAVE_SECCOMP_FILTER -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -Wall -Wextra -O2)
include_directories(
        proot
        proot/cli
        proot/execve
        proot/extension
        proot/extension/care
        proot/extension/portmap
        proot/extension/python
        proot/loader
        proot/path
        proot/ptrace
        proot/syscall
        proot/tracee
        proot/lib/uthash/include/

        talloc/
        talloc/lib/replace/
        talloc/bin/default/
#
#        libarchive/libarchive/

)

add_library(${CMAKE_PROJECT_NAME} SHARED
        proot/loader/assembly.S
        proot/loader/loader.c

        proot/cli/cli.c
        proot/cli/note.c
        proot/cli/proot.c
        proot/execve/enter.c
        proot/execve/exit.c
        proot/execve/shebang.c
        proot/execve/elf.c
        proot/execve/ldso.c
        proot/execve/auxv.c
        proot/execve/aoxp.c
        proot/path/binding.c
        proot/path/glue.c
        proot/path/canon.c
        proot/path/f2fs-bug.c
        proot/path/path.c
        proot/path/proc.c
        proot/path/temp.c
        proot/syscall/seccomp.c
        proot/syscall/syscall.c
        proot/syscall/chain.c
        proot/syscall/enter.c
        proot/syscall/exit.c
        proot/syscall/sysnum.c
        proot/syscall/socket.c
        proot/syscall/heap.c
        proot/syscall/rlimit.c
        proot/tracee/tracee.c
        proot/tracee/mem.c
        proot/tracee/reg.c
        proot/tracee/event.c
        proot/tracee/seccomp.c
        proot/tracee/statx.c
        proot/ptrace/ptrace.c
        proot/ptrace/user.c
        proot/ptrace/wait.c
        proot/extension/extension.c
        proot/extension/ashmem_memfd/ashmem_memfd.c
        proot/extension/kompat/kompat.c
        proot/extension/fake_id0/chown.c
        proot/extension/fake_id0/chroot.c
        proot/extension/fake_id0/getsockopt.c
        proot/extension/fake_id0/sendmsg.c
        proot/extension/fake_id0/socket.c
        proot/extension/fake_id0/open.c
        proot/extension/fake_id0/unlink.c
        proot/extension/fake_id0/rename.c
        proot/extension/fake_id0/chmod.c
        proot/extension/fake_id0/utimensat.c
        proot/extension/fake_id0/access.c
        proot/extension/fake_id0/exec.c
        proot/extension/fake_id0/link.c
        proot/extension/fake_id0/symlink.c
        proot/extension/fake_id0/mk.c
        proot/extension/fake_id0/stat.c
        proot/extension/fake_id0/helper_functions.c
        proot/extension/fake_id0/fake_id0.c
        proot/extension/hidden_files/hidden_files.c
        proot/extension/mountinfo/mountinfo.c
        proot/extension/port_switch/port_switch.c
        proot/extension/sysvipc/sysvipc.c
        proot/extension/sysvipc/sysvipc_msg.c
        proot/extension/sysvipc/sysvipc_sem.c
        proot/extension/sysvipc/sysvipc_shm.c
        proot/extension/link2symlink/link2symlink.c
        proot/extension/fix_symlink_size/fix_symlink_size.c

#        talloc/lib/replace/cwrap.c
#        talloc/lib/replace/replace.c
#        talloc/talloc.c
#
#        native-lib.cpp

)

target_link_libraries(${CMAKE_PROJECT_NAME}
        android
        log
)

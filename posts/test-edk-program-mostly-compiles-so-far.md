<!-- 
.. title: Test EDK program mostly compiles so far
.. slug: test-edk-program-mostly-compiles-so-far
.. date: 2014-11-16 19:09:36 UTC-08:00
.. tags: linux,emotiv,sdk,compiling troubles,test program
.. link: 
.. description: 
.. type: text
.. author: phora
-->

While we were working on our homework, I decided to try writing a test program that would simply. A lot of the code is just copied from ```/opt/EmotivResearch_2.0.0.20/doc/examples_Qt/example1/main.cpp```. The Makefile for the program was written from scratch. Here were the instructions I ran to compile it.

	make clean
	env LD_LIBRARY_PATH=/opt/EmotivResearch_2.0.0.20/lib make
	env LD_LIBRARY_PATH=/opt/EmotivResearch_2.0.0.20/lib ./test-bin

Running the second of the former commands produces the following output:

	g++ -g -I/opt/EmotivResearch_2.0.0.20/include -L/opt/EmotivResearch_2.0.0.20/lib -o test-bin main.c -L/opt/intel/composer_xe_2015.0.090/compiler/lib/intel64 -L/opt/intel/composer_xe_2015.0.090/mkl/lib/intel64 -lcryptopp_64 -ludev -lmkl_rt -liomp5 -lboost_serialization -lboost_system -lboost_regex -lboost_filesystem -lpng12 -lQtCore -lQtGui -ledk_utils_linux -ledk 
	/usr/bin/ld: warning: libboost_serialization.so.1.51.0, needed by /opt/EmotivResearch_2.0.0.20/lib/libedk.so, may conflict with libboost_serialization.so.1.56.0
	/usr/bin/ld: warning: libboost_system.so.1.51.0, needed by /opt/EmotivResearch_2.0.0.20/lib/libedk.so, may conflict with libboost_system.so.1.56.0
	/usr/bin/ld: warning: libboost_regex.so.1.51.0, needed by /opt/EmotivResearch_2.0.0.20/lib/libedk.so, may conflict with libboost_regex.so.1.56.0
	/usr/bin/ld: warning: libboost_filesystem.so.1.51.0, needed by /opt/EmotivResearch_2.0.0.20/lib/libedk.so, may conflict with libboost_filesystem.so.1.56.0


Running the second of the former commands with -lboost_md5 added to the list of link flags produces a peculiar error even though the *.so is in one of the -L'd directories

	g++ -g -I/opt/EmotivResearch_2.0.0.20/include -L/opt/EmotivResearch_2.0.0.20/lib -o test-bin main.c -L/opt/intel/composer_xe_2015.0.090/compiler/lib/intel64 -L/opt/intel/composer_xe_2015.0.090/mkl/lib/intel64 -lcryptopp_64 -ludev -lmkl_rt -liomp5 -lboost_serialization -lboost_system -lboost_md5 -lboost_regex -lboost_filesystem -lpng12 -lQtCore -lQtGui -ledk_utils_linux -ledk 
	/usr/bin/ld: cannot find -lboost_md5
	collect2: error: ld returned 1 exit status
	Makefile:7: recipe for target 'test-bin' failed
	make: *** [test-bin] Error 1


However, ```ls -l /opt/EmotivResearch_2.0.0.20/lib``` shows the following output:

	total 9.4M
	104K -rwxrwxr-x 1  500  500 102K Oct 22 12:44 libboost_filesystem.so.1.51.0*
	 12K -rwxrwxr-x 1  500  500  11K Oct 22 12:44 libboost_md5.so.1.51.0*
	952K -rwxrwxr-x 1  500  500 950K Oct 22 12:44 libboost_regex.so.1.51.0*
	464K -rwxrwxr-x 1  500  500 461K Oct 22 12:44 libboost_serialization.so.1.51.0*
	 12K -rwxrwxr-x 1  500  500  12K Oct 22 12:44 libboost_system.so.1.51.0*
	   0 lrwxrwxrwx 1  500  500   18 Jul 15  2013 libcryptopp_64.so -> libcryptopp.so.1.0*
	   0 lrwxrwxrwx 1  500  500   17 Jul 15  2013 libcryptopp.so.1 -> libcryptopp_64.so*
	4.8M -rwxr-xr-x 1  500  500 4.8M Oct 22 12:44 libcryptopp.so.1.0*
	   0 lrwxrwxrwx 1  500  500   15 Jul 15  2013 libedk.so -> libedk.so.1.0.0*
	   0 lrwxrwxrwx 1  500  500   15 Jul 15  2013 libedk.so.1 -> libedk.so.1.0.0*
	   0 lrwxrwxrwx 1  500  500   15 Jul 15  2013 libedk.so.1.0 -> libedk.so.1.0.0*
	3.1M -rwxrwxr-x 1  500  500 3.1M Oct 22 12:44 libedk.so.1.0.0*
	4.0K -rwxrwxrwx 1  500  500 3.8K Oct 22 12:44 libedk_utils_linux.so*
	   0 lrwxrwxrwx 1 root root   19 Oct 22 12:44 libqwt.so.5 -> /usr/lib/libqwt5.so*
	   0 lrwxrwxrwx 1 root root   15 Oct 22 12:44 libudev.so.0 -> /lib/libudev.so*
	   0 lrwxrwxrwx 1 root root   12 Oct 18 14:27 libudev.so.1 -> libudev.so.0*

I initially shrugged off the output warnings that ld gave me until I tried connecting the test program to the EmoComposer. It crashed because it couldn't find the reference to libboost_md5

	GNU gdb (GDB) 7.8
	Copyright (C) 2014 Free Software Foundation, Inc.
	License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
	This is free software: you are free to change and redistribute it.
	There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
	and "show warranty" for details.
	This GDB was configured as "x86_64-unknown-linux-gnu".
	Type "show configuration" for configuration details.
	For bug reporting instructions, please see:
	<http://www.gnu.org/software/gdb/bugs/>.
	Find the GDB manual and other documentation resources online at:
	<http://www.gnu.org/software/gdb/documentation/>.
	For help, type "help".
	Type "apropos word" to search for commands related to "word"...
	Reading symbols from env...(no debugging symbols found)...done.
	(gdb) run LD_LIBRARY_PATH=/opt/EmotivResearch_2.0.0.20/lib ./test-bin
	Starting program: /usr/bin/env LD_LIBRARY_PATH=/opt/EmotivResearch_2.0.0.20/lib ./test-bin
	Got object file from memory but can't read symbols: File truncated.
	warning: Could not load shared library symbols for linux-vdso.so.1.
	Do you need "set solib-search-path" or "set sysroot"?
	process 7092 is executing new program: /home/shadowkyogre/School/csce499a/test-proggy/test-bin
	warning: Could not load shared library symbols for linux-vdso.so.1.
	Do you need "set solib-search-path" or "set sysroot"?
	warning: the debug information found in "/opt/intel/composer_xe_2015.0.090/compiler/lib/intel64/libiomp5.dbg" does not match "/opt/intel/composer_xe_2015.0.090/compiler/lib/intel64/libiomp5.so" (CRC mismatch).

	[Thread debugging using libthread_db enabled]
	Using host libthread_db library "/usr/lib/libthread_db.so.1".
	===================================================================
	Example to show how to log the EmoState from EmoEngine/EmoComposer.
	===================================================================
	Press '1' to start and connect to the EmoEngine                    
	Press '2' to connect to the EmoComposer                            
	>> 2
	[New Thread 0x7fffed887700 (LWP 7097)]
	Start receiving EmoState! Press any key to stop logging...


	Program received signal SIGSEGV, Segmentation fault.
	[Switching to Thread 0x7fffed887700 (LWP 7097)]
	0x00007ffff4a214c7 in void EmoEventPackage::serialize<boost::archive::text_iarchive>(boost::archive::text_iarchive&, unsigned int) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	(gdb) bt
	#0  0x00007ffff4a214c7 in void EmoEventPackage::serialize<boost::archive::text_iarchive>(boost::archive::text_iarchive&, unsigned int) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#1  0x00007ffff6a221d5 in boost::archive::detail::basic_iarchive::load_object(void*, boost::archive::detail::basic_iserializer const&) () from /usr/lib/libboost_serialization.so.1.56.0
	#2  0x00007ffff4a1ffd9 in void SerializedObjectConnection::handle_read_data<EmoEventPackage, boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> > >(boost::system::error_code const&, EmoEventPackage&, boost::tuples::tuple<boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> >, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type>) ()
	   from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#3  0x00007ffff4a297c9 in boost::asio::detail::read_op<boost::asio::basic_stream_socket<boost::asio::ip::tcp, boost::asio::stream_socket_service<boost::asio::ip::tcp> >, boost::asio::mutable_buffers_1, boost::asio::detail::transfer_all_t, boost::_bi::bind_t<void, boost::_mfi::mf3<void, SerializedObjectConnection, boost::system::error_code const&, EmoEventPackage&, boost::tuples::tuple<boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> >, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type> >, boost::_bi::list4<boost::_bi::value<SerializedObjectConnection*>, boost::arg<1> (*)(), boost::reference_wrapper<EmoEventPackage>, boost::_bi::value<boost::tuples::tuple<boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> >, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type> > > > >::operator()(boost::system::error_code const&, unsigned long, int) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#4  0x00007ffff4a29e02 in boost::asio::detail::reactive_socket_recv_op<boost::asio::mutable_buffers_1, boost::asio::detail::read_op<boost::asio::basic_stream_socket<boost::asio::ip::tcp, boost::asio::stream_socket_service<boost::asio::ip::tcp> >, boost::asio::mutable_buffers_1, boost::asio::detail::transfer_all_t, boost::_bi::bind_t<void, boost::_mfi::mf3<void, SerializedObjectConnection, boost::system::error_code const&, EmoEventPackage&, boost::tuples::tuple<boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> >, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type> >, boost::_bi::list4<boost::_bi::value<SerializedObjectConnection*>, boost::arg<1> (*)(), boost::reference_wrapper<EmoEventPackage>, boost::_bi::value<boost::tuples::tuple<boost::_bi::bind_t<void, boost::_mfi::mf1<void, RemoteEmoEventClient, boost::system::error_code const&>, boost::_bi::list2<boost::_bi::value<RemoteEmoEventClient*>, boost::arg<1> (*)()> >, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type, boost::tuples::null_type> > > > > >::do_complete(boost::asio::detail::task_io_service*, boost::asio::detail::task_io_service_operation*, boost::system::error_code const&, unsigned long) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#5  0x00007ffff4a2ac3c in boost::asio::detail::task_io_service::run(boost::system::error_code&) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#6  0x00007ffff4a18094 in RemoteEmoEventClient::run() () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#7  0x00007ffff4a084e9 in Emotiv::EmotivThreadProc(void*) () from /opt/EmotivResearch_2.0.0.20/lib/libedk.so.1
	#8  0x00007ffff3a14314 in start_thread () from /usr/lib/libpthread.so.0
	#9  0x00007ffff3d113ed in clone () from /usr/lib/libc.so.6
	(gdb) quit
	A debugging session is active.

		Inferior 1 [process 7092] will be killed.

	Quit anyway? (y or n) y

At least we can still write a rudimentary AI while trying to figure out why g++ isn't picking up the libboost_md5 from the Emotiv SDK tarball.

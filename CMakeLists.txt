cmake_minimum_required(VERSION 3.8)
project(couchbase_python_client_2_3_1)

set(LCB_ROOT ../libcouchbase)
set(LCB_ROOT_SRC ${LCB_ROOT}/src)
set(LCB_ROOT_CONTRIB ${LCB_ROOT}/contrib)

set(PYTHON_INCLUDE_DIR /Users/ellis_breen/root/virtualenvs/3.6/default/include/python3.6m/)
set(PYTHON_INCLUDE ${PYTHON_INCLUDE_DIR})
set(LCB_IO ${LCB_ROOT}/src/lcbio)
aux_source_directory(${LCB_ROOT}/src LCB_CORE)
aux_source_directory(${LCB_ROOT}/src/http HTTP)
aux_source_directory(${LCB_ROOT}/include/memcached/ MCD_INC)
aux_source_directory(${LCB_ROOT}/include/libcouchbase/ LCB_INC)
aux_source_directory(${LCB_ROOT}/contrib/lcb-jsoncpp LCB_JSON)
aux_source_directory(${LCB_ROOT}/src/ssl LCB_SSL)
aux_source_directory(${LCB_ROOT}/src/mcserver LCB_MCSERVER)
aux_source_directory(${LCB_IO} LCB_IO_A)
aux_source_directory(${LCB_ROOT_SRC}/sasl LCB_SASL)

aux_source_directory(LCB_VBUCKET ${LCB_ROOT}/src/vbucket)
aux_source_directory(LCB_SASL ${LCB_ROOT}/contrib/cbsasl)
aux_source_directory(LCB_CLI ${LCB_ROOT}/contrib/cliopts)
aux_source_directory(LCB_ROOT_A ${LCB_ROOT_SRC})


ADD_LIBRARY(netbuf OBJECT ${LCB_NETBUF_SRC})
ADD_LIBRARY(netbuf-malloc OBJECT ${LCB_NETBUF_SRC})
ADD_LIBRARY(mcreq OBJECT ${LCB_MC_SRC})
ADD_LIBRARY(rdb OBJECT ${LCB_RDB_SRC})
ADD_LIBRARY(lcbio OBJECT ${LCB_IO_SRC})
ADD_LIBRARY(lcbio-cxx OBJECT ${LCB_IO_CXXSRC})
ADD_LIBRARY(lcbht OBJECT ${LCB_HT_SRC})
ADD_LIBRARY(lcbcore OBJECT ${LCB_CORE_SRC})
ADD_LIBRARY(lcbcore-cxx OBJECT ${LCB_CORE_CXXSRC})
include_directories( ${LCB_CORE}
        ${LCB_ROOT}/include
        ${MCD_INC}
        ${HTTP}
        ${PYTHON_INCLUDE_DIR}
        ${LCB_JSON}
        ${LCB_SSL}
        ${LCB_MCSERVER}
        ${LCB_IO}
        ${LCB_VBUCKET}
        ${LCB_SASL}
        ${LCB_CLI}
        ${LCB_ROOT_SRC}
        ${LCB_SASL}
        ${LCB_SASL}/src
        ${LCB_ROOT_CONTRIB}
        )
include(ExternalProject)

ExternalProject_Add(libcouchbase
        DOWNLOAD_COMMAND ""
        SOURCE_DIR ${LCB_ROOT}
        )
set(CMAKE_CXX_STANDARD 11)
set(EXTRA_SOURCE_DIRS
        ${LCB_ROOT}/src
        ${LCB_ROOT}/include/memcached
        ${LCB_ROOT}/include/libcouchbase
        ${LCB_ROOT}/src/http
        ${LCB_ROOT}/src/ssl

        ${LCB_MCSERVER}
        ${LCB_IO}

        ${LCB_VBUCKET}
        ${LCB_SASL}
        ${LCB_CLI}
        ${LCB_ROOT_SRC}
        ${LCB_ROOT_A}
        )

set(SOURCE
        ${SOURCE}
        ${LCB_CORE}
        ${LCB_INC}
        ${MCD_INC}
        ${HTTP}
        ${LCB_SSL}
        ${LCB_ROOT}/src/ssl

        ${LCB_MCSERVER}
        ${LCB_IO}

        ${LCB_VBUCKET}
        ${LCB_SASL}
        ${LCB_CLI}
        ${LCB_ROOT_SRC}
        )
link_directories(${LCB_ROOT}/lib)
link_libraries(${LCB_ROOT}/../lib/
        )
add_executable(couchbase_python_client_2_3_1
        ${EXTRA_SOURCE_DIRS}
        ${LCB_CORE}
        ${LCB_INC}
        ${MCD_INC}
        ${LCB_JSON}
        ${LCB_SSL}
        ${LCB_ROOT}/src/ssl

        ${LCB_IO}
        ${LCB_VBUCKET}
        ${LCB_SASL}
        ${LCB_CLI}
        ${LCB_ROOT_SRC}
        acouchbase/tests/asyncio_tests.py
        acouchbase/tests/fixtures.py
        acouchbase/tests/py34only.py
        acouchbase/tests/py35only.py
        acouchbase/__init__.py
        acouchbase/asyncio_iops.py
        acouchbase/bucket.py
        acouchbase/iterator.py
        couchbase/async/__init__.py
        couchbase/async/bucket.py
        couchbase/async/events.py
        couchbase/async/n1ql.py
        couchbase/async/rowsbase.py
        couchbase/async/view.py
        couchbase/iops/__init__.py
        couchbase/iops/base.py
        couchbase/iops/select.py
        couchbase/tests/admin/__init__.py
        couchbase/tests/cases/__init__.py
        couchbase/tests/cases/admin_t.py
        couchbase/tests/cases/append_t.py
        couchbase/tests/cases/arithmetic_t.py
        couchbase/tests/cases/badargs_t.py
        couchbase/tests/cases/cbftstrings_t.py
        couchbase/tests/cases/cluster_t.py
        couchbase/tests/cases/connection_t.py
        couchbase/tests/cases/connstr_t.py
        couchbase/tests/cases/datastructures_t.py
        couchbase/tests/cases/delete_t.py
        couchbase/tests/cases/design_t.py
        couchbase/tests/cases/dupkeys_t.py
        couchbase/tests/cases/empty_key_t.py
        couchbase/tests/cases/encodings_t.py
        couchbase/tests/cases/endure_t.py
        couchbase/tests/cases/enh_err_t.py
        couchbase/tests/cases/excextra_t.py
        couchbase/tests/cases/flush_t.py
        couchbase/tests/cases/format_t.py
        couchbase/tests/cases/get_t.py
        couchbase/tests/cases/health_t.py
        couchbase/tests/cases/iops_t.py
        couchbase/tests/cases/itertypes_t.py
        couchbase/tests/cases/itmops_t.py
        couchbase/tests/cases/ixmgmt_t.py
        couchbase/tests/cases/lock_t.py
        couchbase/tests/cases/lockmode_t.py
        couchbase/tests/cases/misc_t.py
        couchbase/tests/cases/mutationtokens_t.py
        couchbase/tests/cases/n1ql_t.py
        couchbase/tests/cases/n1qlstrings_t.py
        couchbase/tests/cases/observe_t.py
        couchbase/tests/cases/pipeline_t.py
        couchbase/tests/cases/results_t.py
        couchbase/tests/cases/rget_t.py
        couchbase/tests/cases/set_converters_t.py
        couchbase/tests/cases/set_t.py
        couchbase/tests/cases/spatial_t.py
        couchbase/tests/cases/stats_t.py
        couchbase/tests/cases/subdoc_t.py
        couchbase/tests/cases/touch_t.py
        couchbase/tests/cases/transcoder_t.py
        couchbase/tests/cases/verinfo_t.py
        couchbase/tests/cases/view_iterator_t.py
        couchbase/tests/cases/view_t.py
        couchbase/tests/cases/viewstrings_t.py
        couchbase/tests/cases/xattr_t.py
        couchbase/tests/__init__.py
        couchbase/tests/base.py
        couchbase/tests/importer.py
        couchbase/tests/test_sync.py
        couchbase/views/__init__.py
        couchbase/views/iterator.py
        couchbase/views/params.py
        couchbase/__init__.py
        couchbase/_bootstrap.py
        couchbase/_ixmgmt.py
        couchbase/_libcouchbase.cpython-36m-darwin.so
        couchbase/_logutil.py
        couchbase/_pyport.py
        couchbase/_version.py
        couchbase/admin.py
        couchbase/auth_domain.py
        couchbase/bucket.py
        couchbase/bucketmanager.py
        couchbase/cbas.py
        couchbase/cluster.py
        couchbase/connection.py
        couchbase/connstr.py
        couchbase/exceptions.py
        couchbase/experimental.py
        couchbase/fulltext.py
        couchbase/items.py
        couchbase/mockserver.py
        couchbase/mutation_state.py
        couchbase/n1ql.py
        couchbase/priv_constants.py
        couchbase/result.py
        couchbase/subdocument.py
        couchbase/transcoder.py
        couchbase/user_constants.py
        examples/abench.py
        examples/basic.py
        examples/bench.py
        examples/connection-pool.py
        examples/docloader.py
        examples/gbench.py
        examples/iops_demo.py
        examples/item.py
        examples/reversed_keys.py
        examples/search_keywords.py
        examples/twist-sample.py
        examples/txbasic.py
        examples/txbench.py
        examples/txview.py
        gcouchbase/tests/__init__.py
        gcouchbase/tests/test_api.py
        gcouchbase/tests/test_gevent.py
        gcouchbase/__init__.py
        gcouchbase/bucket.py
        gcouchbase/connection.py
        gcouchbase/iops_gevent0x.py
        gcouchbase/iops_gevent10.py
        src/bucket.c
        src/callbacks.c
        src/cntl.c
        src/connevents.c
        src/constants.c
        src/convert.c
        src/counter.c
        src/ctranscoder.c
        src/exceptions.c
        src/ext.c
        src/fts.c
        src/get.c
        src/htresult.c
        src/http.c
        src/iops.c
        src/iops.h
        src/ixmgmt.c
        src/miscops.c
        src/mresdict.h
        src/multiresult.c
        src/n1ql.c
        src/observe.c
        src/opresult.c
        src/oputil.c
        src/oputil.h
        src/pipeline.c
        src/pycbc.h
        src/result.c
        src/store.c
        src/typeutil.c
        src/views.c
        txcouchbase/tests/__init__.py
        txcouchbase/tests/base.py
        txcouchbase/tests/test_n1ql.py
        txcouchbase/tests/test_ops.py
        txcouchbase/tests/test_txconn.py
        txcouchbase/tests/test_views.py
        txcouchbase/__init__.py
        txcouchbase/bucket.py
        txcouchbase/connection.py
        txcouchbase/iops.py
        couchbase_version.py
        setup.py)

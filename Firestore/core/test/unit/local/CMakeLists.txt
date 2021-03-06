# Copyright 2018 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(
  local_testing_sources
  counting_query_engine.cc
  counting_query_engine.h
  persistence_testing.cc
  persistence_testing.h
)

firebase_ios_add_library(
  firestore_local_testing
  EXCLUDE_FROM_ALL
  ${local_testing_sources}
)

target_link_libraries(
  firestore_local_testing PRIVATE
  firestore_core
)


firebase_ios_glob(
  sources *.cc *.h
  EXCLUDE ${local_testing_sources}
)
firebase_ios_add_test(firestore_local_test ${sources})

target_link_libraries(
  firestore_local_test PRIVATE
  GMock::GMock
  firestore_core
  firestore_local_testing
  firestore_protos_protobuf
  firestore_remote_testing
  firestore_testutil
)

---
layout: post
title: C++ Evolution
date: 2020-06-13 16:15
category: 
author: Prasanth Kanna
tags: [C++]
description: Brief info on all the changes in every iteration of C++
image: cpp_evolution/cpp_evolution.jpg
---

Complete history of C++

[Early C++](#early-c++)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C with Classes(1979)](#c-with-classes(1979))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++(1985)](#c++(1985))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++2.0(1989 & 1990)](#c++2.0(1989-&-1990))

[Standard C++](#standard-c++)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++98(1998)](#c++98(1998))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++03(2003)](#c++03(2003))

[Modern C++](#modern-c++)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++11(2011)](#c++11(2011))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++14(2014)](#c++14(2014))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++17(2017)](#c++17(2017))

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[C++20(2020)](#c++20(2020))

# Early C++

## C with classes(1979)

* classes
* Member Functions
* Derived Classes
* Separate Compilation
* Public and Private access control
* Friends
* Type checking of function arguments
* Default arguments
* Inline functions
* Overloaded assignment operator
* Constructors
* Destructors
* f() same as f(void)

## C++(1985)

Features:

* Virtual functions
* Function and operator overloading
* References
* New and delete operators
* The keyword const
* Scope resolution operator
* Single-line comments

Libraries:

* complex
* string
* iostream

## C++2.0(1989 & 1990)

Features:

* Multiple inheritance
* Pointers to members
* Protected access
* Type-safe linkage
* Abstract classes
* Static and const member functions
* Class-specific new and delete
* Namespaces
* Exception handling
* Nested classes
* Templates
* New casts
* Boolean type

Libraries:

* I/O manipulators

# Standard C++

## C++98(1998)

Features:

* RTTI (dynamic_cast
* typeid)
* Covariant return types
* Cast operators
* Mutable
* Bool
* Declarations in conditions
* Template instantiations
* Member templates
* Export

Libraries:

* locales
* bitset
* valarray
* auto_ptr
* templatized string
* iostream
* complex.

STL:

* containers
* algorithms
* iterators
* function objects

## C++03(2003)

Features:

* Value initialization

# Modern C++

## C++11(2011)

Language features:

* auto and decltype
* defaulted and deleted functions
* final and override
* trailing return type
* rvalue references
* move constructors and move assignment operators
* scoped enums
* constexpr and literal types
* list initilization
* delegating and inherited constructors
* brace-or-equal initializers
* nullptr
* long long
* char16_t and char32_t
* type aliases
* variadic templates
* generalized (non-trivial) unions
* generalized PODs (trivial types and standard-layout types)
* Unicode string literals
* user-defined literals
* attributes
* lambda expressions
* noexcept specifier and noexcept operator
* alignof and alignas
* multithreaded memory model
* thread-local storage
* GC interface
* range-for (based on a Boost library)
* static_assert (based on a Boost library)

Headers

* \<typeindex>
* \<type_traits>
* \<chrono>
* \<initializer_list>
* \<tuple>
* \<scoped_allocator>
* \<cstdint>
* \<cinttypes>
* \<system_error>
* \<cuchar>
* \<array>
* \<forward_list>
* \<unordered_set>
* \<unordered_map>
* \<random>
* \<ratio>
* \<cfenv>
* \<regex>
* \<atomic>
* \<thread>
* \<mutex>
* \<future>
* \<condition_variable>

Library features

* atomic operations library
* emplace() and other use of rvalue references throughout all parts of the existing library
  * std::unique_ptr
  * std::move_iterator
* s  d::initializer_list
* s  ateful and scoped allocators
* s  d::forward_list
* chrono library
* ratio library
* new algorithms
* Unicode conversion facets
* thread library
* std::exception_ptr
* std::error_code and std::error_condition
* iterator improvements:
  * std::begin
  * std::end
  * std::next
  * std::prev
* Unicode conversion functions

## C++14(2014)

Language features

* variable templates
* generic lambdas
* lambda captures expressions
* new/delete elision
* relaxed restrictions on constexpr functions
* binary literals
* digit separators
* return type deduction for functions
* aggregate classes with default non-static member initializers.

Library features

* std::make_unique:
* std::shared_timed_mutex and std::shared_lock
* std::integer_sequence
* std::exchange
* std::quoted
* and many small improvements to existing library facilities
 such as
  * two-range overloads for some algorithms
  * type alias versions of type traits
  * user-defined string
  * duration
  * and complex number literals
  * etc.

## C++17(2017)

Obsolete:

Removed

* auto_ptr
* deprecated function objects
* std::random_shuffle
* std::unexpected
* the obsolete iostreams aliases
* trigraphs
* the register keyword
* bool increment

Deprecated

* std::iterator
* std::raw_storage_iterator
* std::get_temporary_buffer
* std::is_literal_type
* std::result_of
* all of \<codecvt>

Language features:

* fold-expressions
* class template argument deduction
* auto non-type template parameters
* compile-time if constexpr
* inline variables
* structured bindings
* initializers for if and switch
* u8-char
* simplified nested namespaces
* using-declaration can declare multiple names
* made noexcept part of type system
* new order of evaluation rules
* guaranteed copy elision
* lambda capture of *this
* constexpr lambda
* attribute namespaces don't have to repeat
* new attributes [[fallthrough]] [[nodiscard]] and [[maybe_unused]]
* __has_include

Headers:

* \<any>
* \<optional>
* \<variant>
* \<memory_resource>
* \<string_view>
* \<charconv>
* \<execution>
* \<filesystem>

Library features:

In utility

* tuple:
  * apply
  * deduction_guides
  * make_from_tuple
* variant
* launder
* to_chars/from_chars
* as_const
* searchers
* optional
* any
* not_fn

In memory

* uninitialized memory tools
  * destroy_at
  * destroy
  * destroy_n
  * uninitialized_move
  * uninitialized_value_construct
* weak_from_this
* polymorphic allocators
* aligned_alloc
* transparent owner_less
* array support for shared_ptr
* allocation functions with explicit alignment
* variadic lock_guard
* cache line interface

In types

* byte
* conjunction/disjunction/negation
* type trait variables xxx_v
* is_swappable
* is_invocable
* is_aggregate
* has_unique_object_representations.

In algorithm

* clamp
* execution policies
* reduce
* inclusive_scan
* exclusive_scan

container related

* map/set extract and map/set merge
* map/unordered_map try_emplace and insert_or_assign
* contiguous iterators
* non-member size/empty/data

In numeric

* mathematical special functions
* gcd
* lcm
* 3D hypot

Other

* is_always_lock_free
* uncaught_exceptions
* timespec_get
* rounding functions for duration and time_point

## C++20(2020)

Language features

* Feature test macros
* 3-way comparison operator <=> and operator==() = default
* designated initializers
* init-statements and initializers in range-for
* char8_t
* [[no_unique_address]]
* [[likely]]
* [[unlikely]]
* pack-expansions in lambda captures
* removed the requirement to use typename to disambiguate types in many contexts
* consteval, constinit
* further relaxed constexpr
* signed integers are 2's complement
* aggregate initialization using parentheses
* Coroutines
* Modules
* Constraints and concepts
* Abbreviated function templates
* DR: array new can deduce array size

Library features

Headers

* \<concepts>
* \<coroutine>
* \<compare>
* \<version>
* \<source_location>
* \<format>
* \<span>
* \<ranges>
* \<bit>
* \<numbers>
* \<syncstream>
* in Thread support library:
* \<stop_token>
* \<semaphore>
* \<latch>
* \<barrier>

Library features

* Formatting library
* Calendar and Time Zone library
* std::source_location
* std::span
* std::endian
* array support for std::make_shared
* std::remove_cvref
* std::to_address
* floating point and shared_ptr atomics
* std::barrier, std::latch, and std::counting_semaphore
* std::jthread and thread cancellation classes
* \<version>
* std::osyncstream
* std::u8string and other char8_t uses
* constexpr for \<algorithm>, \<utility>, \<complex>
* std::string::starts_with / ends_with and * std::string_view::starts_with / ends_with
* std::assume_aligned
* std::bind_front
* std::c8rtomb/std::mbrtoc8
* std::make_obj_using_allocator etc
* std::make_shared_for_overwrite/std::make_unique_for_overwrite
* heterogeneous lookup in unordered associative containers
* std::polymoprhic_allocator with additional member functions and * std::byte as its default template argument
* std::execution::unseq
* std::midpoint and std::lerp
* std::ssize
* std::is_bounded_array, std::is_unbounded_array
* Ranges
* uniform container erasure (std::erase/std::erase_if)
* Mathematical constants
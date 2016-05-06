# Embed Resource

Embed binary files and resources (such as GLSL Shader source files) into
C++ projects. Uses C++11 features and Boost for filesystem.

Include this repository in your CMake based project:

    git submodule add https://github.com/darrenmothersele/embed-resource.git lib/embed-resource

Then add to your CMakeLists.txt for your project:

    include_directories(lib/embed-resource)
    add_subdirectory(lib/embed-resource)

Now you can add your resources, by calling the provided `embed_resources()` function:

    embed_resources(MyResources shaders/vertex.glsl shaders/frag.glsl)

Then link to your binary:

    add_executable(MyApp ${SOURCE_FILES} ${MyResources})

In your C++ project you can access your embed resources using the Resource class
provided in `Resource.h`. Here's an example:

    #include <iostream>
    using namespace std;

    #include "Resource.h"

    int main() {

        Resource text = LOAD_RESOURCE(frag_glsl);
        cout << string(text.data(), text.size()) << endl;

        return EXIT_SUCCESS;
    }

NB: To reference the file, replace the `.` in `frag.glsl` with an underscore `_`.
So, in this example, the symbol name is `frag_glsl`.

### Credits...

This uses ideas based on
[this](https://beesbuzz.biz/blog/e/2014/07/31-embedding_binary_resources_with_cmake_and_c11.php)
and [this](http://stackoverflow.com/questions/11813271/embed-resources-eg-shader-code-images-into-executable-library-with-cmake).

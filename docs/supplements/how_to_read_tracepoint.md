以下の図ではトレースポイントがどのようにして追加され、読み込まれてるかを示しています。

![how to add tracepoint](../../imgs/function_call.png)

ROS 2の各層でどのようにトレースポイントを追加しているかを示しています。

galacticは全ての層で直接ROS 2を書き換えて追加しています。

CARETはrclcpp層のヘッダーで定義されている関数は直接ROS 2を書き換えています。

それ以外の層はLD_PRELOADのフックを用いてトレースポイントを追加しています。

以下の図ではpublish()とDDS_write()がどのようにしてトレースポイント関数を追加されているかを示しています。

![how to read tracepoint](../../imgs/tracepoint_location.png)

直接書き換える方法では、関数内に処理が追記されています。
それに対して、フックの方法では.soライブラリ内の関数が呼ばれ、その中に元の関数を呼ぶ処理とトレースポイントの処理が入っています。

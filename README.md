# ffmpeg-nvenc

* nvidiaのGPUを使ったh.264，h.265形式のエンコードを可能にしたffmpegのDockerfileです．
* nvidia-docker2をインストールしておく

# Dockerイメージのビルド

```bash
git clone https://github.com/myoshimi/ffmpeg-nvenc
cd ffmpeg-nvenc
docker build -t ffmpeg-nvenc .
```

# エンコード例

## GPUを使ってh.265形式でエンコード

```bash
docker run --rm --runtime=nvidia \
    -v ${PWD}:/tmp/ ffmpeg-nvenc:latest \
    -stats \
    -i /tmp/bbb_sunflower_1080p_60fps_normal.mp4 \
    -vcodec hevc_nvenc \
    /tmp/bbb_sunflower_1080p_60fps_normal_h265.mp4
```

## その他オプション

vcodecオプションを変更すると，コーデックを変更できます．

| Processor | codec | -vcodec    |
|-----------|-------|------------|
| CPU       | H.265 | libx264    |
| CPU       | H.264 | libx265    |
| GPU       | H.265 | hevc_nvenc |
| GPU       | H.264 | h264_nvenc |


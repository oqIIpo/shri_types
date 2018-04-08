[TS](https://www.typescriptlang.org/play/index.html#src=const%20hasOwnProperty%3A%20(x%3A%20string)%20%3D%3E%20boolean%20%3D%20Object.prototype.hasOwnProperty%3B%0D%0Aconst%20_toString%3A%20()%20%3D%3E%20string%20%3D%20Object.prototype.toString%3B%0D%0A%0D%0Afunction%20isPlainObject(obj%3A%20any)%3A%20boolean%20%7B%0D%0A%20%20if%20(_toString.call(obj)%20!%3D%3D%20%22%5Bobject%20Object%5D%22)%20%7B%0D%0A%20%20%20%20return%20false%3B%0D%0A%20%20%7D%0D%0A%0D%0A%20%20const%20prototype%20%3D%20Object.getPrototypeOf(obj)%3B%0D%0A%20%20return%20prototype%20%3D%3D%3D%20null%20%7C%7C%20prototype%20%3D%3D%3D%20Object.prototype%3B%0D%0A%7D%0D%0A%0D%0Ainterface%20SomeObj%20%7B%0D%0A%20%20%5Bkey%3A%20string%5D%3A%20any%3B%0D%0A%7D%0D%0A%0D%0Ainterface%20ExtendFunc%20%7B%0D%0A%20%20(arg0%3A%20boolean%20%7C%20SomeObj%2C%20arg1%3F%3A%20SomeObj%2C%20...rest%3A%20SomeObj%5B%5D)%3A%20SomeObj%3B%0D%0A%7D%0D%0A%0D%0Aconst%20extend%3A%20ExtendFunc%20%3D%20(arg0%20%3D%20false%2C%20arg1%20%3D%20%7B%7D%2C%20...rest)%20%3D%3E%20%7B%0D%0A%20%20let%20target%3A%20SomeObj%3B%0D%0A%20%20let%20deep%3A%20boolean%3B%0D%0A%20%20let%20extendObjects%3A%20object%5B%5D%20%3D%20rest%3B%0D%0A%0D%0A%20%20if%20(typeof%20arg0%20%3D%3D%3D%20%22boolean%22)%20%7B%0D%0A%20%20%20%20deep%20%3D%20arg0%3B%0D%0A%20%20%20%20target%20%3D%20arg1%3B%0D%0A%20%20%7D%20else%20%7B%0D%0A%20%20%20%20deep%20%3D%20false%3B%0D%0A%20%20%20%20target%20%3D%20arg0%3B%0D%0A%20%20%20%20extendObjects.push(arg1)%3B%0D%0A%20%20%7D%0D%0A%0D%0A%20%20for%20(let%20i%20%3D%200%3B%20i%20%3C%20extendObjects.length%3B%20i%2B%2B)%20%7B%0D%0A%20%20%20%20const%20obj%20%3D%20rest%5Bi%5D%3B%0D%0A%20%20%20%20for%20(const%20key%20in%20obj)%20%7B%0D%0A%20%20%20%20%20%20if%20(hasOwnProperty.call(obj%2C%20key))%20%7B%0D%0A%20%20%20%20%20%20%20%20const%20val%3A%20any%20%3D%20obj%5Bkey%5D%3B%0D%0A%20%20%20%20%20%20%20%20const%20isArray%20%3D%20val%20%26%26%20Array.isArray(val)%3B%0D%0A%20%20%20%20%20%20%20%20%2F%2F%20%D0%9A%D0%BE%D0%BF%D0%B8%D1%80%D1%83%D0%B5%D0%BC%20%22%D0%BF%D0%BB%D0%BE%D1%81%D0%BA%D0%B8%D0%B5%22%20%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D1%8B%20%D0%B8%20%D0%BC%D0%B0%D1%81%D1%81%D0%B8%D0%B2%D1%8B%20%D1%80%D0%B5%D0%BA%D1%83%D1%80%D1%81%D0%B8%D0%B2%D0%BD%D0%BE.%0D%0A%20%20%20%20%20%20%20%20if%20(deep%20%26%26%20val%20%26%26%20(isPlainObject(val)%20%7C%7C%20isArray))%20%7B%0D%0A%20%20%20%20%20%20%20%20%20%20const%20src%20%3D%20target%5Bkey%5D%3B%0D%0A%20%20%20%20%20%20%20%20%20%20let%20clone%3B%0D%0A%20%20%20%20%20%20%20%20%20%20if%20(isArray)%20%7B%0D%0A%20%20%20%20%20%20%20%20%20%20%20%20clone%20%3D%20src%20%26%26%20Array.isArray(src)%20%3F%20src%20%3A%20%5B%5D%3B%0D%0A%20%20%20%20%20%20%20%20%20%20%7D%20else%20%7B%0D%0A%20%20%20%20%20%20%20%20%20%20%20%20clone%20%3D%20src%20%26%26%20isPlainObject(src)%20%3F%20src%20%3A%20%7B%7D%3B%0D%0A%20%20%20%20%20%20%20%20%20%20%7D%0D%0A%20%20%20%20%20%20%20%20%20%20target%5Bkey%5D%20%3D%20extend(deep%2C%20clone%2C%20val)%3B%0D%0A%20%20%20%20%20%20%20%20%7D%20else%20%7B%0D%0A%20%20%20%20%20%20%20%20%20%20target%5Bkey%5D%20%3D%20val%3B%0D%0A%20%20%20%20%20%20%20%20%7D%0D%0A%20%20%20%20%20%20%7D%0D%0A%20%20%20%20%7D%0D%0A%20%20%7D%0D%0A%20%20return%20target%3B%0D%0A%7D%3B%0D%0A%0D%0Aextend(%7B%7D%2C%20%5B1%2C3%5D))


[Flow](https://flow.org/try/#0MYewdgzgLgBAFgQwgeQO5gAoCcQAcCmWUAngFwwAU0WAlmAOYCUMAvAHwwBGIIANvgjCsYyTgCt8wKADpcOKCBIFpiFOmx5CJANwAoUJFgKAylFoNyFQcWbsY1OvWGiJU2fMXFlJs4726AegAqIN0YIJhAfBBAARBAPhBAJhBAVhBowHkQRMAhEAAaGEBxEHTYmEB+EGTEwBYQQAYQQF4QSsBpEEBOEBhYwEYQQCkQRMAuEHSYFPjAbhA09MBBEBSYACJC3tjB9sAOEEAeEFHKdOlE6RhB2MB2EArqmrn1oti52MBJEEAZEEA5EDGAbwBfUbCImd6ZsbB8VBFxSShRxmlHo8YAABXAILAIAC2MGuLh+txgIHEQOBWHwUAArlhIDCAEI8fiCW6PAK6ABmGLAUho4BgNAgGF4CDocKkFCRYnI1kY5G4fAEQmuYRgIpoZMoPnM9GkwAQvF47PEzAAhCwWDAAOQAbQ5Py+rigAF0NcwhSLzea0ZjsTAyXKIPg9BbicKRQZoDA5IpPARnN83PR0RoFEp8MgyYqxIwnZb0VihF6Q158Kw1TAwBj5TAAD7Z10Wz0eUOp9WsmSJn2O3Qu4KhcIwQBYILFCjNooBhEAyRRKORmgxecxqiXW8VidUG6Xi5UapUqsUAzCAFZ6vSqJaaxXpnWaAURBGq0Ovl4jBD4AxEESvUSI4azTanQB4RRYIh0Ou+P5RJgWoAJvh8LgWHbeAdQ0omiV5NkqcockSSoZleAADMwMXwODh1HcdJxgdpm1bNsLiGEZog6NtokGGZ4lnO8IlBcEoRhMsESgcFA1gQA8ED3ToYFKfoYGicpBkACRBW2gmYUjWFjKkOXo2x7LpZ3iQdULHCdykokFH1o65pC0+jEX9KAIBgNib3SGp1gKQZL3Q8o5leLiRiwls4knGDRJgQAEEGiOc2zmaCTLMmBwMg4SUhsoECzgjN5RQpcYDgylvzJOh8E-aK51nUD2zw4ZVNRONsQM2E9OJcJSWLYwQEhMNxGEa4tQcBgc3TDFIU4QhDS5MBiARXR9HAD18AADygfAwE-YQKSpKAaSEQbhtGgAeAAVchysqlw2CsLB6AABl5AkBUaxbsi06QmIgcgAEEsAhYglo4U1834IwmPRPa3yEbMYEW4QmO2mMRSemBv1-N7CTAf6YEBmhyAzFrCH8C0AgCQyml4ppyhMydEn2Uj0jbcpjxmK45ykppYiwhdMOwpyqhEu9zTFCVkxAcVGK29ES01PkwZNGF8wtYHcGENnmIhi0RY59Uzq1bbDTFhnhAARghhF8EAlMzQLEVBfG+0qy10VhD+-MXQtMkQCwShtDpGB5pgM7pH4BgoDga2aAAandh6DZgd1YA5chvqlraIC1Gg5f5hnxQoZUOW9n3zQMKaM31g3usjgBIDOkb9mAAGt8GIAzSz06QC6LyNGEjrXzctihc-LukhDjvmE4NxmKFUNBMBwAgiGIGU5QVDlsnLxh47bn3c4ANzlQPhA5LVy4jyeE9z+krpu4RZ94GAADI95gTeEAHjfrpPigd+jHrV59pHG2pjt9nGSZphmRJFmvfdTNeOY+NI+SPEiIkTIhRaut8O46wPjAHe+9D4UHpIyZkYAyyXzlMwXMdIIDHxsBPW+U8+qwAgFgYAwsXpQCXoXFe+CE6A2ALwcAqcaHt2jmfG6eDmFTwYe8YQxDSHQJwdINhF8+HMAAPz2BITAcgWpqGcILKrdWrd5Fr24SmdUfC4FYKQSyPSVASHiMkaQ8gdx5byOKio8W5DKHEGAuqWaI1PwUEFtkehjDshXzMbfRRDplGWJFBLChy9t5yi8avCx+CIkJyiRnE2N9YzWiEIEvQtw9BAA)

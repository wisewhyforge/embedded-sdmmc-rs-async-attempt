impl<'a, D, T, const MAX_DIRS: usize, const MAX_FILES: usize, const MAX_VOLUMES: usize> Drop
    for Volume<'a, D, T, MAX_DIRS, MAX_FILES, MAX_VOLUMES>
where
    D: crate::BlockDevice,
    T: crate::TimeSource,
{
    fn drop(&mut self) {
        
        _ = self.volume_mgr.close_volume(self.raw_volume)
    }
}

I commented out the above code in lib.rs this was in response to close_volume not being awaited and basically doing nothing. I don't know what upstream affects there may be from doing this

The tests should be ignored as the test functions cannot be async